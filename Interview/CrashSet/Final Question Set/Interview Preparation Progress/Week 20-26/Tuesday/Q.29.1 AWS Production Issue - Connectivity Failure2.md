# AWS Production Issue - Connectivity Failure

## Situation

A production application was unable to communicate with a dependent service hosted in AWS.

## Task

My responsibility was to identify whether the issue was application, network, or security-related.

## Action

I checked application logs and monitoring alerts to understand the failure.

I validated connectivity between servers and checked security group rules, network configuration, and DNS resolution.

I found that the issue was related to a security group rule change that was blocking communication.
I coordinated with the network team to update the required rule, validated connectivity, and confirmed the application was working normally

## Result

The connectivity was restored, and the application recovered successfully.
