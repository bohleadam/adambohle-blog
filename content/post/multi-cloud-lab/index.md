---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Multi Cloud Lab - Introduction"
subtitle: "The mother of all demo labs"
summary: "Part 1 - We are building out a Multi-Cloud Demo lab. Have a read about what we are doing"
authors: [admin]
tags: []
categories: []
date: 2021-03-25T10:44:05Z
lastmod: 2021-03-25T10:44:05Z
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: "center"
  preview_only: true

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

One area that I have been working on recently, with my colleagues in the VMware Multi-Cloud field team, is the build out of a Multi-Cloud lab environment to show how the presence of VMware Cloud Foundation offerings in all of the major public cloud providers, can enable a multi-cloud solution for customers.

I wanted to talk a little here around what we are creating, and what we have planned in terms of setup and architecture for this lab. As we build the lab out and put together new multi-cloud use cases, we will look to document them publicly, and I plan to create a series of blog articles here around what we are doing.

{{% alert note %}}
This blog series is not intended to be a step by step guide in terms of deploying out individual components, please reference product documentation for those steps. However I will call out any steps which are undocumented or need further clarification.
{{% /alert %}}

Our current lab bill of materials (BOM) consists of the following components;

1. 3 x Node [VMware Cloud on AWS](https://cloud.vmware.com/vmc-aws) SDDC running in AWS us-west-2 (Oregon)
2. 3 x Node [Azure VMware Solution](https://azure.microsoft.com/en-gb/services/azure-vmware/) Private Cloud (SDDC) running in Azure EAST US (Virginia)
3. 3 x Node [Google Cloud VMware Engine](https://cloud.google.com/vmware-engine) Private Cloud (SDDC) running in Google US-WEST-2 (Southern California)
4. An On-premise vSphere 7.0.1 SDDC running in Chicago
5. Cloud Interconnect services provided by [Megaport](https://www.megaport.com)

We plan to have additional capacity and representation from other public cloud providers later on, for the moment, this will just have to do ;)

Being able to run a consistent VMware Cloud Foundation based infrastructure in each of these major hyper-scale public cloud providers offers a clear advantage to those who are looking to operate a hybrid cloud infrastructure between their on-premise data center, and a public cloud provider. As customers find themselves in more than one public cloud provider, the desire for consistency across these locations grows.

What we are seeing more and more from customers now is the challenge of operating both their on-premise datacenter, which for many customers, is not going away entirely, along with multiple public cloud offerings

Operating different technology stacks, different configuration formats, different services etc etc, this is becoming a well understood challenge now for anyone looking to consume these different technologies. As technology teams look to manage all of these multi-cloud silos, many technology vendors in the market are looking to address this issue. From a VMware perspective, we are looking to address multi-cloud across all areas of the IT landscape.

**Infrastructure**

**Operations**

**Developer Experience**

Consistent Infrastructure and Operations is key for every customer I speak to, the prospect of re-platforming and the re-architecture of all applications and introducing risk, cost, and delays to consuming public cloud infrastructure is a real concern. Having the option to simply use the same technologies which run their business today, is a major benefit. The obvious and clear benefits of being able to move workloads through technologies such as Hybrid Cloud Extension (HCX) from a vSphere platform on-premise, to a VMware Cloud Foundation powered SDDC running in a global hyper-scale public cloud provider is compelling. But from a multi-cloud perspective, we now offer customers the freedom to move workloads to multiple cloud providers, as well as giving customers the ability to move to one cloud provider, with the real option to move workloads out of that provider and onto another provider later on, should they choose to do so. No re-platforming, no re-factoring, no changes to IP addresses, no risk.

Keeping that same infrastructure layer has a knock on affect to every layer above it, the same operations processes and procedures, no re-tooling required. Existing management tooling see's just another vCenter/NSX endpoint. Developers are able to consume infrastructure for traditional applications and modern application architectures making use of the [Tanzu Portfolio](https://tanzu.vmware.com) of solutions.

So what are we actually building.

Lets take a look at the below high level overview which shows what we are putting together here;

{{< figure src="https://bohleadam-blog-assets.s3.eu-west-2.amazonaws.com/multi-cloud-high-level-01.jpg"title="multi-cloud-hld" >}}
*Slide credit to - John Marrone, VMware*

I appreciate this is a high level "Marketing Style" depiction. Myself and the team will produce more detailed overviews as we develop this lab environment out.

You can expect more detailed content in the following areas

1. Networking overviews and how we connected all of these different public cloud providers.
2. Automation used to stand-up each of these SDDC environments.
3. How we can enable application mobility across between public clouds running VMware Cloud Foundation.
4. Build, Run, Manage, Connect and Protect all of your traditional and modern architecture applications across any cloud.

So stay tuned, we will be producing more content on this topic in the future. If you have anything you would like to see in this lab, any use cases you think we should explore, please leave a comment below.
