---
title: "gst-validate: A suite of tools to run integration tests for GStreamer"
date: 2014-04-21
slug: gst-validate-a-suite-of-tools-to-run-integration-tests-for-gstreamer
guid: https://blogs.gnome.org/tsaunier/2014/04/21/gst-validate-a-suite-of-tools-to-run-integration-tests-for-gstreamer-2/
source: wordpress
---

<a href="http://www.collabora.com/" class="external">Collabora ltd.</a> has been developing a tool that allows GStreamer developers to check that the GstElements they write behave the way they are supposed to: GstValidate. The tool was started first to provide plug-ins developers with a tool to check that they use the framework the proper way. Since the beginning, it has been available in <a href="http://cgit.freedesktop.org/gstreamer/gst-devtools/" class="external">gst-devtools</a>, a gst module where we collect a set of tools to facilitate GStreamer development and usage.

# Well, what is it about?

## The GstValidateMonitor

Basically gst-validate allows us to monitor everything that is happening inside a <a href="http://gstreamer.freedesktop.org/data/doc/gstreamer/head/gstreamer/html/GstPipeline.html" class="external">GstPipeline</a>. For example if you want to check that every component of a pipeline is properly behaving, you can create a GstValidatePipelineMonitor that will track that pipeline. Then each time a GstElement is added to the pipeline, a GstValidateElementMonitor will be instantiated and start tracking that element. Then when a GstPad is added to that GstElement a GstValidatePadMonitor will be monitoring that pad.

This monitoring logic allows us to check that what those elements do respect some rules GStreamer components have to follow so all the elements of a pipeline can properly interact together. For example, a GstValidatePadMonitor will make sure that if we receive a GstSegment from upstream, an equivalent segment is sent downstream before any buffer gets out. You can find the whole list of tests currently implemented <a href="http://cgit.freedesktop.org/gstreamer/gst-devtools/tree/validate/gst/validate/gst-validate-report.c#n87" class="external">here</a>.

## The GstValidateRunner

Then there is an issue reporting system so that each issue found during the execution of the pipeline is reported with as much details as possible so that users understand what the detected misbehaviour is about and can fix it efficiently.

In term of code the only thing to do in order to get a pipeline monitored is:

    int
    main (int argc, gchar ** argv)
    {
     GstElement *pipeline;
     GstValidateRunner *runner;
     GstValidateMonitor *monitor;

     gboolean ret = 0;

     /* Initialize GStreamer and GstValidate */
     gst_init (&argc, &argv);
     gst_validate_init ();

     /* Create the pipeline and make sure it is
      * monitored */
     pipeline = gst_pipeline_new (
         "monitored-pipeline");
     runner = gst_validate_runner_new ();
     monitor = gst_validate_monitor_factory_create (
         GST_OBJECT (pipeline),
         runner,
         NULL);

     /* HERE you can do anything you want with that
      * monitored pipeline */

     /* Now print the errors on stdout.
      * The return value of that function
      * is != 0 if if critical errors occured
      * during the execution of the pipeline */
     ret = gst_validate_runner_printf (runner);

     /* Cleanup */
     gst_object_unref (pipeline);
     gst_object_unref (monitor);
     gst_object_unref (runner);

     return ret;
    }

The result of gst_validate_runner_printf will look something like:

    issue : buffer is out of the segment range Detected on theoradec0.srcpad at 0:00:00.096556426
            
    Details : buffer is out of segment and shouldn't be pushed. Timestamp: 0:00:25.000 - duration: 0:00:00.040 Range: 0:00:00.000 - 0:00:04.520
    Description : buffer being pushed is out of the current segment's start-stop  range. Meaning it is going to be discarded downstream without any use

Here we can see that an issue occurred on the src pad of theoradec as it outputted a buffer that was not inside the segment it last pushed. This is an interesting piece of information and clearly shows an error in the element. (Note: This issue does not actually exist)

# How should it be used?

## GstValidate command line tools

In order to make gst-validate usage simple, we created command line tools that allow plugin developers test there elements in many use cases from a high level perspective.

### The gst-validate pipeline launcher

This is a command line pipeline launcher similar to gst-launch. That tool uses the gst-launch pipeline description syntax and make sure that the pipeline is monitored and that the users will have all the reported information from the GstValidate infrastructure. As you can expect, you can monitor the playback of a media file using [playbin](gstreamer.freedesktop.org/data/doc/gstreamer/head/gst-plugins-base-plugins/html/gst-plugins-base-plugins-playbin.html) as follow:

    gst-validate-1.0 playbin uri=file:///.../file.ogg

You will then be able to see all the issues GstValidate found.

### The gst-validate-transcoding tool

A command line tool allowing to test media files transcoding with a straight forward syntax. You can for example transcode any media file to vorbis vp8 in webm doing:

    gst-validate-transcoding-1.0 
        file:///./file.ogg 
        file:///.../transcoded.webm 
        -o 'video/webm:video/x-vp8:audio/x-vorbis'

It will report what issues happened during the execution of that pipeline.

### The gst-validate-media-check tool

A command line tool checking that media files discovering works properly with <a href="http://gstreamer.freedesktop.org/data/doc/gstreamer/head/gst-plugins-base-libs/html/gst-plugins-base-libs-gstdiscoverer.html" class="external">gst-discoverer</a>. Basically it needs a reference text file containing valid information about a media file (which can be generated with the same tool) and then it will be able to check that those informations correspond to what is reported by gst-discoverer over new runs.  For example, given that we have a valid reference.media_info file, we can run:

    gst-validate-media-check-1.0 
      file:///./file.ogv 
      --expected-results reference.media_info

That will then output found errors if any and return an exist code different from 0 if an error was found.

### GstValidateScenarios

As you can notice, those tools let us test static pipelines execution and not that the pipeline reacts properly during execution of actions from the end user such as seeking, or changing the pipeline state, etc… In order to make that possible and easy to use we introduced the concept of scenarios.

A scenario is a set of actions to be executed on the monitored pipeline serialized in a text file. An  action (GstValidateAction) is just a function call executed at a precise time (usually based on the playback position of the pipeline).

An example of scenario:

    # Just some metadatas describing the scenario
    # The format is the GstStructure serialization 
    # synthax
    description, seek=true, duration=3.0

    # When the pipeline reaches 1.0 second of
    # playback it launches an accurate flushing
    # seek to 10.0 seconds
    seek, playback_time=1.0, start=10.0, 
    flags=accurate+flush

    # Send EOS to the pipeline
    # so it stops and the application
    # knows about it.
    eos, playback_time=12.0

You can find more examples of scenarios <a href="http://cgit.freedesktop.org/gstreamer/gst-devtools/tree/validate/data" class="external">here</a>

## gst-validate-launcher

This looks all right but shouldn’t those tests be executed automatically on a large number of samples and with the various existing scenarios? This is where gst-validate-launcher comes into play. It is basically a python application that launches the tools described above with the proper parameters. It then monitors them, check their results and serializes those results into a junit xml file (more formatter could obviously be implemented). That tools is pretty simple and it is only a matter of setting the media samples to run the tests on and set what scenarios you want to run.

# Where is it used?

## GStreamer Editing Services

As part of the <a href="http://wiki.pitivi.org/wiki/GES" class="external">GStreamer Editing Services</a> project, I have made sure that ges-launch (a command line tool that launches timelines, video editing projects etc…) works with GstValidate, if compiled against it. This means that we can launch scenarios and test GES sharing the same infrastructure as the rest of GStreamer. It is also very interesting to be able to monitor dynamic pipeline (within GES the GstPipeline changes very dynamically) to discover elements misbehavior in that stressful use case. For the time being we do not have many GES specific GstValidateActions implemented, but we will implement more as needed (mostly implementing timeline edition actions, ie. moving clips around the timeline, changing effect properties, etc…) As part of the <a href="http://fundraiser.pitivi.org" class="external">Pitvi fundraiser</a>, we are also investigating how to serialize users action in <a href="http://pitivi.org" class="external">Pitivi</a> so that we could easily reproduce users issues outside of the application (and thus outside the python interpreter).

## The GStreamer jenkins integration server

On the <a href="https://jenkins.arracacha.collabora.co.uk" class="external">GStreamer continuous integration</a> server, we are <a href="https://jenkins.arracacha.collabora.co.uk/view/pitivi/job/gst-validate-tests/" class="external">running gst-validate-launcher</a> on a set of media sample in major formats after (almost) each commit on any of the component of the GStreamer stack. This is just the beginning and we are slowly adding more tests there making sure they pass and tracking regressions.

A lot of work has been done around that tool. We still need to clean up some part, review the few APIs we have, and a particular effort as to be made around the documentation. But now that good basis are there, we should just keep adding more tests to detect regressions in GStreamer as soon as possible. If you are interested in using that tool please come talk to us in \#gstreamer on freenode!
