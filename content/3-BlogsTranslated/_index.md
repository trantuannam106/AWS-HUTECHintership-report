---
title: "Translated Blogs"
date: 2026-07-02
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

###  [Blog 1 - Accessing Amazon S3 Privately from a VPC using a VPC Endpoint](3.1-Blog1/)
This blog guides you on how to design a secure architecture to access Amazon S3 privately from within a VPC without relying on Public IPs, Internet Gateways, or NAT Gateways. You will explore practical scenarios of deploying internal backend microservices or data processing workloads inside private subnets, and understand how a Gateway VPC Endpoint works alongside route tables to safely route traffic within the internal AWS network. Additionally, the post emphasizes a defense-in-depth security mindset by combining IAM Roles, Endpoint policies, and Bucket policies under the principle of least privilege to ensure a system that is both smooth to operate and highly secure.

### [Blog 2 - Amazon CloudFront – Accelerating Content Delivery from Edge to Origin](https://www.google.com/search?q=3.2-Blog2/)
This blog post introduces how to use Amazon CloudFront to solve the issues of inconsistent page load speeds and high latency when users access web applications from various geographic regions. You will learn why AWS's Content Delivery Network (CDN) is crucial for caching diverse content (static files, videos, APIs), how it significantly reduces the load on origin servers (like Amazon S3 or EC2), and its capability to enhance security when combined with AWS WAF. The article also guides you through the basic hands-on steps to create a CloudFront Distribution, configure the origin, customize cache behavior, and test actual page load speeds.

###  [Blog 3 - ...](3.3-Blog3/)
This blog introduces how to start building a data lake in the healthcare sector by applying a microservices architecture. You will learn why data lakes are important for storing and analyzing diverse healthcare data (electronic medical records, lab test data, medical IoT devices…), how microservices help make the system more flexible, scalable, and easier to maintain. The article also guides you through the steps to set up the environment, organize the data processing pipeline, and ensure compliance with security & privacy standards such as HIPAA.
