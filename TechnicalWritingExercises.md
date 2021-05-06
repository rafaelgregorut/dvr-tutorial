# Technical Writing Exercises

Author: Rafael Mota Gregorut
Markdown file:

## Tech Writing Exercise 1

### Introduction

This tutorial explains the basic playback functions of the Digital Video Recorder (DVR) and how to record a TV show. This tutorial does not explain how to install the DVR. 

|DVR Front Panel|DVR Remote Control|
|-|-|
|![DVR frontal panel](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/DVRFrontPanel.png?raw=true) <br/>_The DVR has a minimalist front panel._|![DVR remote control](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/RemoteControlHorizontal_min.png?raw=true) <br/>_The remote control allows you to access the DVR functions._|

### DVR Playback Functions
The DVR has the following playback functions accessible through the remote control: 

* Play ![The Play button on the remote control](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/PlayIcon.png?raw=true) 
* Pause ![The Pause button on the remote control](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/PauseIcon.png?raw=true) 
* Stop ![The Stop button on the remote control](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/StopIcon.png?raw=true) 
* Rewind ![The Rewind button on the remote control](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/RewindIcon.png?raw=true) 
* Fast-forward ![The Fast-forward button on the remote control](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/FFIcon.png?raw=true) 

To use one of the playback fucntions, press the respective button on the remote control. 
In the next section, let's go through the steps to record a TV show. 

### How To Record a TV Show
Take the following steps to record a TV show: 
1. Press the Guide button ![Press the Guide button on the remote control.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/GuideButton.png?raw=true) on the remote control. 
2. Use the arrow buttons ![Use the arrow buttons on the remote control to navigate through the TV guide.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/ArrowsButtons.png?raw=true) on the remote control to navigate through the TV guide. 
3. Select the TV show you want to record. 

    ![Select the TV show you want to record.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/TV1.png?raw=true) 
    _The TV guide allows you to navigate through channels and check their schedules._ 
4. Press the Record button ![Press the Record button on the remote controll.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/RecordIcon.png?raw=true) on the remote control. 
5. Select Yes in the dialog. 

    ![Select Yes in the dialog.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/Dialog.png?raw=true) 
    _Confirm that you wish to record the selected TV show._ 
5. Press the OK button ![](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/OKButton.png?raw=true) on the remote control to confirm. 
6. Check that the Record icon is displayed on the TV show you selected to record. 

    ![Check that the Record icon is displayed on the TV show.](https://github.com/rafaelgregorut/dvr-tutorial/blob/main/media/TV2.png?raw=true) 
    _The TV guide displays the Record icon on the TV show that is set to be recorded._ 

Once these steps are performed, the selected TV show is set to be recorded. 

----
## Tech Writing Exercise 2

This article contains insights from the optmization benchmark study of 2010. It presents general concepts and issues of the Ehcache cluster replication, and how to solve them with ClusterLink, a new Liferay Portal Enterprise Edition (EE) feature. 

Ehcache supports clusters and by default uses RMI replication, which is a point-to-point communication. This solution is not scalable for a large system since each cluster sends the same event to all other clusters, causing a traffic issue. 

For each cache entity, Ehcache creates a replication thread that consumes memory and CPU power. For example, in a system with 100 cache entities: 
* The system will create 100 threads. 
* The system will consume 200MB of stack memory, considering a thread stack size of 2MB. 
* A single node of the system might consume 500MB of heap memory. 

An optimized solution should consider following points: 

* The majority of the threads are likely inactive for most of the time and only start working when they need to communicate with remote peers. 
* The high number of threads frequently causes an overhead to switch context. 

Although a newer Ehcache version supports JGroups' Replicator and solves the communication traffic, it does not solve the thread replication problem. 

ClusterLink, an EE feature, solves both the communication traffic and thread replication problems. ClusterLink is an abstract communication channel that implements by default a JGroups' UDP multicast. 

ClusterLink provides a dedicate group of dispatching threads to deliver cache cluster events to remote peers. Since all events will go through one channel, ClusterLink merges modifications to the same cache object that are close enough and notifies remote peers only once. 

Please contact our support engineers for more details on ClusterLink. 

----
## Tech Writing Exercise 3

```java
/**
* Returns the concatenation of the base String up to the offset, 
* the inserted String and the remaining part of the base String.
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
* @param insert the String to be inserted into the base String.
* Initial spaces in the String to be inserted are ignored.
*
* @param offset the index in the base String where to place the 
* second String
*
* @return the concatenation of the base String up to the offset, 
* the inserted String and the remaining part of the base String.
* Returns <code>null</code> if the base String is <code>null</code>.
*
*/
public static String insert(String s, String insert, int offset) {
    ...
}
```