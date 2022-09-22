---
layout: post
title: How Shecan Works
slug: how-shecan-works
---

If you are not familiar with Shecan, you can visit [Shecan's website](https://shecan.ir).

A little while ago, I used Shecan to install Docker on a new Ubuntu server machine.
As it was doing its thing, I wondered how does Shecan works.
So I searched for the answer and found nothing!
Actually, Shecan does mention how it works on its FAQ page, but it is not very clear.

![Shecan's FAQ page](/assets/images/2022-09-22-how-shecan-works/shecan-faq.png)

So I decided to dig deeper and find out how Shecan actually works. 

## The FAQ Answer is partially correct

As mentioned in the FAQ, Shecan works based on DNS.
But DNS just translates domain names to IP addresses and it does not do anything about ditching blocked websites.
So Shecan is not a normal DNS server.
Actually, Shecan translates blocked websites domain names to IP addresses of its own servers and then it proxies the traffic to the original website.

## How I figured it out

I resolved Docker Hub registry (which is blocked in Iran) address once with Google DNS and once with Shecan DNS.

![DNS resolution](/assets/images/2022-09-22-how-shecan-works/docker-hub-ip.png)

Then I used [db-ip.com](https://db-ip.com) to find some information about the IP addresses.

The IP addresses resolved by Google DNS are owned by Amazon AWS; which is a logical place for the Docker Hub. But the IP addresses resolved by Shecan DNS are owned by someone named **Ebrahim Mohammadi**.

![IP addresses information](/assets/images/2022-09-22-how-shecan-works/db-ip.png)

A quick search on LinkedIn shows that Ebrahim Mohammadi is the founder of Bonyan Co. which is the company behind Shecan. Eureka!