# Technical Writing Exercises

Author: Rafael Mota Gregorut

## Tech Writing Exercise 1

### Introduction

This tutorial explains the basic playback functions of the Digital Video Recorder (DVR) and how to record a TV show. This tutorial does not explain how to install the DVR.

|DVR Front Panel|DVR Remote Control|
|-|-|
|![DVR frontal panel](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/DVRFrontPanel.png?raw=true)|![DVR remote control](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/RemoteControlHorizontal_min.png?raw=true)|

### DVR Playback Functions
The DVR has the following playback functions accessible through the remote control:

* Play ![](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/PlayIcon.png?raw=true)
* Pause ![](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/PauseIcon.png?raw=true)
* Stop ![](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/StopIcon.png?raw=true)
* Rewind ![](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/RewindIcon.png?raw=true)
* Fast-forward ![](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/FFIcon.png?raw=true)

### How To Record a TV Show
Take the following steps to record a TV show:
1. Press the Guide button ![Press the Guide button on the remote control.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/GuideButton.png?raw=true) on the remote control.
2. Use the arrow buttons ![Use the arrow buttons on the remote control to navigate through the TV guide.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/ArrowsButtons.png?raw=true) on the remote control to navigate through the TV guide.
3. Select the TV show you want to record.

    ![Select the TV show you want to record.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/TV1.png?raw=true)
4. Press the Record button ![Press the Record button on the remote controll.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/RecordIcon.png?raw=true) on the remote controll.
5. Select Yes in the dialog.

    ![Select Yes in the dialog.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/Dialog.png?raw=true)
5. Press the OK button ![](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/OKButton.png?raw=true)  on the remote control to confirm.
6. Check that the Record icon is displayed on the TV show.

    ![Check that the Record icon is displayed on the TV show.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/TV2.png?raw=true)

----
## Tech Writing Exercise 2

_This article contains insights from the optmization benchmark study of 2010. It presents general concepts and issues of the Ehcache cluster replication, and how to solve them with ClusterLink, a new Enterprise Edition (EE) feature._

_Ehcache supports clusters and by default uses RMI replication, which is a point-to-point communication. This solution is not scalable for a large number of clusters since each cluster sends the same event to all other clusters._

_For each cache entity, Ehcache creates a replication thread that consumes memory and CPU power. For example, in a system with 100 cache entities:_
* _The system will create 100 threads_
* _The system will consume 200MB of stack memory, considering a thread stack size of 2MB_
* _A single node of the system might consume 500MB of heap memory_

_However, optimized alternatives are possible because of the following reasons:_

* _The majority of the threads are likely inactive for most of the time and only start working when they need to communicate with remote peers_
* _The high number of threads frequently causes an overhead to switch context_

_A newer Ehcache version supports JGroups' Replicator and solves the communication traffic, but it does not solve the thread replication problem._

_ClusterLink, a Liferay EE feature, solves both the communication traffic and thread replication problems. ClusterLink is an abstract communication channel that implements by default a JGroups' UDP multicast._

_ClusterLink provides a dedicate group of dispatching threads to deliver cache cluster events to remote peers. Since all events will go through one channel, ClusterLink merges modifications to the same cache object that are close enough and notifies remote peers only once._

_Please contact our support engineers for more details on ClusterLink._

----
## Tech Writing Exercise 3

```java
/**
* Returns a String with the left part of the base String, 
* the inserted String at the offset index and the right part of the base String. 
* Initial spaces in the inserted String are ignored.
* 
* <p>
* <pre>
* <code>
* StringUtil.insert("happy day", " birth", 6) = "happy birthday"
* StringUtil.insert(null, " birth", 6) = null
* </code>
* </pre>
* </p>
* 
* @param s the base String for the insertion
*
* @param insert the String to be inserted into <code>s</code>
*
* @param offset the index in <code>s</code> where to place <code>insert</code>
*
* @return the new string with the left part of <code>s</code>, 
* the <code>insert</code> placed at the index <code>offset</code> and 
* the right part of <code>s</code>. Returns <code>null</code> if <code>s</code> is <code>null</code>.
*
*/
public static String insert(String s, String insert, int offset) {
    ...
}
```