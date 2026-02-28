Hi everyone. This is my first time doing a public presentation, but I want to keep it vendor-neutral and truly explain what OpenClaw can do. OpenClaw is incredibly powerful overall, but non-technical people-and I know there are quite a few in the room-often do not understand how to even set it up. My goal is to distill the essential information you need to easily set up and start using OpenClaw.

In the spirit of open source, I've released all the slides I'm using today. There is a QR code you can scan at the end of the presentation, so no photos are required.

A quick caveat: given the nature of the audience, I will present this as a "happy path." This means there are edge cases I won't necessarily cover, because even getting a basic 0-to-1 implementation running can unlock many possibilities. Just to be clear on conflicts of interest, I am not sponsored by anyone; my perspective is purely technical.

### **Background & Architecture**

To give a little context about myself, I am a computer engineer from SUTD. I've moved around a bit in my career-I started in product management at Shopee, worked on a few startups, and then moved to a medical tech company where I built products from 0 to 1\. Through these experiences, I hope to give an objective perspective on how to achieve this deployment.

OpenClaw was started by Peter Steinberger. It is an incredible framework because it effectively unlocks the "agent economy," meaning everyone can have a personal assistant on their phone or messaging app. It's incredibly powerful and is currently one of the fastest-growing frameworks out there, recently hitting around 230,000 GitHub stars.

Here is how OpenClaw is structured:

* **SO Document:** Think of this as a way to tell the agent how it should behave. OpenClaw provides a comprehensive SO document (essentially a system prompt). Many people customize this to give the agent a personality that fits their customer persona.  
* **Cron Jobs:** If you check the official documentation, a cron job is effectively a scheduler. If you have an intense task-like parsing a 10,000-row spreadsheet at 9:00 AM every day-you use a cron job.  
* **Heartbeats:** Heartbeats are easily mixed up with cron jobs, but a heartbeat is proactive. For example, you can set the agent to give you proactive updates at 30-minute intervals without you needing to prompt it first.

### **Hosting & Setup Options**

To get an OpenClaw agent running, you need a host. There are three main ways to go about it:

1. **Virtual Machines (VMs):** A raw server where you can run everything freely. This is most applicable for advanced developers.  
2. **Containers:** A Platform-as-a-Service (PaaS) offering provided by vendors like Alibaba Cloud, Google Cloud Platform, or DigitalOcean.  
3. **Serverless/SaaS:** Managed OpenClaw instances where vendors update and maintain the system for you. You just start using it.

### **Choosing a Model & Security**

Next, you need to consider what model (and billing plan) you want to use to power OpenClaw. Here are a few factors to consider:

* **Context Window:** This is how much information an AI model can remember. It has scaled from 128k to about a million tokens, which is amazing for long-running agentic tasks.  
* **Price vs. Performance:** As a bootstrap founder, I focus heavily on cost efficiency. Some developers prefer a "one-shot" approach-writing one prompt to get a perfect result-but that can be expensive.  
* **Security & Gateways:** You must consider domains, ports, and gateways. Assigning the correct port to OpenClaw can be highly technical. Running OpenClaw locally (like on a Mac Mini) without proper guardrails could do harm, which is why managed instances are often better for enterprise scenarios.  
* **Channels & Skills:** OpenClaw supports channels like Telegram, WhatsApp, WeChat, and DingTalk. "Skills" are like downloading apps on your phone to give OpenClaw new functions. Always ensure you are using skills from reliable sources (like Peter Steinberger's 51 built-in skills) to minimize security risks.

### **Live Demo**

Now I'll do a live demo. I'm using Alibaba Cloud to show how to start a simple application server with a managed OpenClaw implementation.

I'll create a fresh virtual machine and apply the latest OpenClaw image (version 226.2.9). For the model setting, Alibaba defaults to M3.5 Plus, though you can switch to models from other frontier labs if you prefer.

Next, I will configure the ports to allow Telegram to connect with this server, execute the configuration plan, and access the OpenClaw Web User Interface (the gateway).  
To pair OpenClaw with Telegram, you first need to use Telegram's BotFather. I'll create a new bot (e.g., openclaw-meetup-test-1-bot) and grab the token. Then, I open the terminal. The word "terminal" might sound concerning to non-technical people, but it's not too difficult. I'll enter the following command:

openclaw channels add telegram \[token\]

So my bot is called openclaw-meetup-test-1-bot. You just click on this to start the bot. If the bot is successfully started...

...you will actually receive a pairing code. The next terminal command to write is simply:  
openclaw pairing approve telegram \[8 digit code\]

Once you are done, the pairing is successful, and you can start chatting with your OpenClaw bot. I like to ask OpenClaw, "What can you do?" so I can understand its capabilities straight from the prompts without looking at the terminal.

That is the fastest way I know to get OpenClaw up and running without using a managed SaaS vendor. If you have a better way, please reach out to me\! Here are my slides \- all open source, just scan the QR code and use them. Given time constraints, I am happy to address your questions offline. I really appreciate it\!