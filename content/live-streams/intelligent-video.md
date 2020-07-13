---
title: "Series: Intelligent Video Analytics with NVIDIA Jetson"
subtitle: 
comments: false
date: 2020-07-10T19:00:00-04:00
tags: ["NVIDIA", "Jetson", "Azure", "MachineLearning", "LiveStream"]
---

Over the past several weeks [Paul DeCarlo](https://twitter.com/pjdecarlo) and I have been working on a [video series](https://www.youtube.com/playlist?list=PLzgEG9tLG-1QLc-DPPABoW1YWFMPNQl4t) and [example project with documentation](https://github.com/toolboc/Intelligent-Video-Analytics-with-NVIDIA-Jetson-and-Microsoft-Azure) on the Intelligent Edge. Where we worked on an Intelligent Video Analytics system using a $99 [NVIDIA Jetson Nano](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-nano/).

The project takes RSTP video feeds from a couple of local security cameras and then uses NVIDIA's DeepStream SDK and Azure's IoT Hub, Stream Analytics, Time Series Insights, and PowerBI to do object detection at the edge on the Nano, collect metrics about the objects scene by the individual cameras, forwards them up to Azure, then presents a dashboard for viewing and querying the analytics we've collected.

This was a fun learning experience for me and much easier to get started with than I expected. I had never done anything surrounding machine learning before.

We closed out the series with a live Twitch stream with members of the [NVIDIA Embedded](https://twitter.com/nvidiaembedded) talking about the Intelligent Edge and the Jetson devices.

## Archive

### Getting Started with NVIDIA Jetson Nano: Object Detection
Erik and Paul configure a Jetson Nano device for use with DeepStream SDK using samples provided from NVIDIA.

Part 1 of a 5 part series created for #JulyOT
{{< youtube yZz-4uOx_Js>}}

### Configure and Deploy "Intelligent Video Analytics" to IoT Edge Runtime on NVIDIA Jetson
Erik and Paul create an Azure IoT Hub and backing storage account in Microsoft Azure, then instrument a Jetson Nano with IoT Edge and configure it with a deployment that uses these services to accommodate an intelligent video analytics solution.

Part 2 of a 5 part series created for #JulyOT 
{{< youtube RKwwP4XsZdw>}}

### Develop and deploy Custom Object Detection Models with IoT Edge DeepSteam SDK Module

Erik and Paul demonstrate how to leverage a model developed with CustomVisionAI for use with the IoT Edge DeepSteam SDK Module and then explore how to employ a Custom Yolo Parser for use with YoloV3 and YoloV3 Tiny.

Part 3 of a 5 part series created for #JulyOT 
{{< youtube kv0eTobemug>}}

### Consuming and Modeling Object Detection Data with Azure Time Series Insights
Erik and Paul forward object detections to Time Series Insights from  an Azure Stream Analytics on the Edge Job.  We showcase the whole process of setting up a TSI event source to modeling and exporting of the data within Time Series Insights.

Part 4 of a 5 part series created for #JulyOT
{{< youtube l5tjaD-qYwY>}}

### Visualizing Object Detection Data in Near Real-Time with PowerBI
Erik and Paul forward results from an Azure Stream Analytics Job into a PowerBI Dataset.  They then develop a custom report for visualizing data in a live PowerBI Dashboard.

Part 5 of a 5 part series created for #JulyOT
{{< youtube lhvPbNF9eb4>}}

### Building the Intelligent Edge with Jetson and Azure ft. the NVIDIA Embedded team
On today’s stream we Erik St. Martin and Paul DeCarlo from the Microsoft Cloud Advocacy team meet with team members from NVIDA to discuss “Building the Intelligent Edge with Jetson and Azure”.  We will be discussing a number of topics related to this theme and will supplement with questions from attendees on the stream.

NVIDIA team members include:
 Chintan Shah, Product Manager
 Tenika Versey, Marketing Lead for AI
 Ryan Huff, Business Development for AI | Edge | IoT
 Jaime Flores, AI Developer Relations Manager
{{< youtube ug_Tw4bKERs>}}