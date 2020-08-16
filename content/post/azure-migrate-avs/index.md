---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Azure Migrate for Azure VMware Solution"
subtitle: "Sizing... I LOVE sizing. Clearly I'm joking, I hate sizing"
summary: "The below article talks about the benefits of accurately sizing for VMware SDDC environments in hyper scale cloud providers, and how Microsoft are working to make this easier"
authors: []
tags: [AVS, Azure, Sizing]
categories: []
date: 2020-08-12T22:08:43+01:00
lastmod: 2020-08-12T22:08:43+01:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: "Center"
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

One of the key considerations when looking at data center exit is, how am i going to size my existing on-premise estate to determine the required footprint in a VMware backed hyperscale cloud offering. Lets face it, it's not the most exciting activity in the world, but it is an activity which, carried out in a rushed fashion, or with out due care and attention. Can result in either an oversized or under sized cloud environment. Now you are probably reading this thinking, "But this is cloud, I pay for what I use." This is true, you can pay on demand and indeed, pay for what you use. However when customers are looking at consuming VMware SDDC technology in a public cloud provider, the number one use case is normally data center exit, and easy migration. With this in mind many customers look to consume the SDDC infrastructure on hosts which are paid for through a reserved instance (RI) commitment model in order to leverage well understood discount models over a 1 or 3 year term.

It's at this point where you want to have a level of accuracy when it comes to how many hosts you plan to commit to. No one wants to be in the position where they are either, explaining why they spent too much money on reserved instances, or justifying why they need to go back to the business and ask for more money because they didn't forecast correctly.

There are various tools out there to collect this type of information. Most VI Admins are familiar with [RVTools](https://www.robware.net/rvtools/), a really handy utility which you can download for free, run against your on-premise environment and quickly get a point in time snapshot of your on-premise vSphere estate from which you can pull metrics such as the;

* Number of VMs
* vCPU allocations
* vRAM allocations
* Storage Allocated and Consumed

From here you can start to see quickly what your estate looks like. The way I explain this to the customers I work with, it's like taking a photograph of you virtual environment.

Other tools which are popular for gathering information include [LiveOptics](https://www.liveoptics.com/). LiveOptics takes this a step further and provides you with collector software which you run on a Windows machine in your environment to monitor vCenter and send the data to LiveOptics to crunch the data and provide you with dashboards and consolidated data which can be fed into a sizing tool to provide insight into the size of the required environment, LiveOptics already has integration with the [vSan Sizer](https://vsansizer.vmware.com/) to automatically ingest this data to size vSan Ready Nodes.

But with this article I wanted to raise awareness of what Microsoft are doing with the [Azure Migrate](https://azure.microsoft.com/en-gb/services/azure-migrate/#features) tool which now allows users to use this tooling to collect all of the relevant data about the on-premise vSphere environment and allow you to create an Assessment of the environment to calculate what you will need in terms of node counts within AVS.

The reason I like this approach comes down to the following issues which occur with sizing.

1. Standardizing on input metrics, very often people will change the input numbers or they will come from outdated on unknown sources. Utilizing a standard automated solution for collecting the correct inputs is essential.
2. Removal of the potential for human error. We all know what can happen when you ask people to perform boring repetitive tasks, human error and the potential for mistakes in sizing activities with a large amount of manual steps creates risk to accuracy.
3. Bias. People are different, people interpret data differently and this has the potential to lead to different outputs when there is potential to adjust inputs, adjust calculations (sometimes this is needed) and interpret results.

Automation of the above is key to removing as much of the above as possible.

So, how does Azure Migrate help with this.

{{% alert note %}}
As of the writing of this article, Azure VMware Solution sizing in Azure Migrate is in Public Preview. If you are sizing for production environments you should wait until Microsoft make this functionality Generally Available (GA).
{{% /alert %}}

For those who are not familiar with Azure Migrate, this is a solution available as a service in Azure that will discover your on premise environment, and assist with migrations. Traditionally this tooling was used to migrate virtual machines to native Azure. But now it has additional functionality to allow you to collect the data that was originally used to inform users on which Azure native instance types to convert their virtual machines to, and now use that same data to size out what an Azure VMware Solution environment will need to be. Answering the issues I raised above

1. Standardize the inputs
2. Remove the human error
3. No bias, let the calculation engine do its thing.

I won't go into the detail around how Azure Migrate works, or how to set this up, you can find that detail by going to the [Azure Migrate Documentation](https://docs.microsoft.com/en-gb/azure/migrate/) and you can find a lot of detail here around the process for [Azure VMware Solution Assessments](https://docs.microsoft.com/en-gb/azure/migrate/concepts-assessment-calculation).

You have choices around how you choose to collect the data. You can either download the pre-built VM as an OVA, or run the scripts and MSI files into installer the collector capabilities on an existing Windows image, or you have the choice to populate a .csv template with the required fields which will be fed into the calculation engine.

{{< figure src="https://bohleadam-blog-assets.s3.eu-west-2.amazonaws.com/Xnip2020-08-13_19-45-55.jpg" title="Discover Virtual Machines in Azure Migrate" >}}

Once the collector is up and running you will see the discovered virtual machines start to appear in the Azure Migrate solution in the Azure Portal

{{< figure src="https://bohleadam-blog-assets.s3.eu-west-2.amazonaws.com/Xnip2020-08-13_20-16-52.jpg" title="List of discovered VMs with basic metrics" >}}

There are other capabilities here around dependency mapping which is useful, and certainly worth considering when you are looking at Migrations, you don't want to leave part of an application behind during a migration and then find you have just introduced higher latency into your application :smile:

Now that we have all this detail we can very easily create an assessment to move those workloads directly to Azure VMware Solution

{{< figure src="https://bohleadam-blog-assets.s3.eu-west-2.amazonaws.com/Xnip2020-08-16_19-34-20.jpg" title="AVS sizing Assessment" >}}

As you can see you can see pricing detail, I have removed this until official pricing is available at General Availability, and you can see the host count you require.

But one thing that is most notable is the Readiness. All of these workloads are ready for Azure, no checking if OS's are supported, no checking if instance availability is going to be an issue. You can simply move the workload to Azure with no changes.

You can essentially, Hit the easy button on moving workloads to Azure VMware Solution.
