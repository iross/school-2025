---
status: testing
---

<style type="text/css"> pre em { font-style: normal; background-color: yellow; } pre strong { font-style: normal; font-weight: bold; color: \#008; } </style>

HTC Exercise 1.6: Remove Jobs From the Queue
===============================================

## Exercise Goal

In the last exercise, we learned how to estimate and request resources needed for our jobs. Imagine a scenario where you realize you've requested the wrong amount of resources after submitting a batch of jobs. You want to remove the jobs from the queue so you can submit them with the correct resource requirements. How do you do that?

The goal of this exercise is to show you how to remove jobs from the queue. This is helpful if you make a mistake, do not want to wait for a job to complete, or otherwise need to fix things. For example, if some test jobs go on hold for using too much memory or disk, you can remove them, edit the submit files, and then submit again.

!!! note
    Please remember to remove any jobs from the queue that you are no longer interested in. Otherwise, the queue will start to get very long with jobs that will waste resources (and decrease your priority), or that may never run (if they're on hold, or have other issues keeping them from matching).

This exercise is short, but if you are out of time, you can come back to it later.

## Removing a Job or Cluster From the Queue

To practice removing jobs from the queue, you need a job in the queue!

1.  Submit a job from an earlier exercise.
1.  Determine the job ID (`cluster.process`) from the `condor_submit` output or from `condor_q`
1.  Remove the job using its full job ID, e.g. `5759.0`.

        :::console
        [username@ap40]$ condor_rm <JOB.ID>

1.  Did the job leave the queue immediately? If not, about how long did it take?

When you use the full job ID, you remove only one job from the batch of jobs (or one process from the cluster of jobs). However, it is possible to remove all jobs that are part of a cluster at once. Simply omit the job process (the `.0` part of the job ID) in the `condor_rm` command:

``` console
[username@ap40]$ condor_rm <CLUSTER>
```

Finally, you can include many job clusters and full job IDs in a single `condor_rm` command. For example:

``` console
[username@ap40]$ condor_rm 5768 5769 5770.0 5771.2
```

## Removing All of Your Jobs

If you really want to remove all of your jobs at once, you can do that with:

```console
[username@ap40]$ condor_rm <USERNAME>
```

If you want to test it: (optional, though you'll likely need this in the future)

1.  Quickly submit several jobs from past exercises
1.  View the jobs in the queue with `condor_q`
1.  Remove them all with the above command
1.  Use `condor_q` to track progress

In case you are wondering, you can remove only your own jobs.
HTCondor administrators can remove anyone’s jobs, so be nice to them. :)
