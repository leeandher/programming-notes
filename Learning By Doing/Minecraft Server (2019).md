# Starting a Minecraft Server (March 2019)

To whoever is reading this, trying to spin up a Minecraft server in 2019 without paying for _Minecraft Realms_, I respect that. My girlfriend recently saw some GIFs or something and wants to start up a server for us to play together, plus I think this could be a fun Saturday experiment. I'm going to talk a little bit about my process in getting this up and running. I'm definitely not used to SSHing into Linux servers but we'll give it a shot.

---

## Step 1: Hosting

While there are plenty of hosting options out there, I'm a pretty cheap guy, so I'll give you my break down of the options. Full Disclosure: I don't know too much about this stuff, AND have no idea what kind of services are offered on MS Azure. So here's my breakdown.

### DigitalOcean

For hosting a persistant Minecraft server, this is probably the best choice. By persistant, I mean without any downtime. You and your friends can login whenever you feel like and the server will always running, ready for you join. DigitalOcean is known for its relative ease of use, and cheap prices, so spinning one up in the cloud to run 24/7 is a great, cost-effective choice.

Note: Droplets on DigitalOcean have no ROM, and therefore, if your service shuts down, you'll lose your server's data. There's definitely a way to copy the data to your local machine before that happens, but that's just another thing to keep in mind.

### Amazon Web Services

Now we're getting into the nitty gritty. AWS is verbose and hosting/using any servers on their platforms is not very easy to get started with. You'll be reading the docs for a few hours before you really feel comfortable getting started, especially considering how easy it is to rack up large bills if you don't know what you're doing. Personally, I would say to choose AWS if you want a non-perstant, secure, cheap server and you're willing to put the time into it. That means having an EC2 instance in the cloud that you can SSH into and spin up your server before you play, and shut it down when you're done. Honestly, it might even be cheaper than DigitalOcean in some cases when runnning full time, but that's up to you.

Note: Similar to before, but with a server that isn't persistant, it's very easy for you to lose all your data since EC2 instances have no ROM to store anything. That means you'll have to ALSO have an S3 bucket to persist data between your gaming sessions, which is a whole other thing to set up. If you ever ditch the server, atleast that bucket will have its contents saved, but that'll cost ya! Probably not hard for an expert, but definitely a challenge for me to get started with, that's why I chose the cheapest alternative.

### Host Machine

If you don't plan on having too many people playing at once, and you know/trust them all, it might be a good idea to dust off that old laptop that sits in the corner of your room. Paying for secure anonynmous server space is great, but so is not having to pay \$5.00 a month to play a game you already have with a bunch of friends. So going forward in this doc, I'm going to help along with how you can set up a seperate machine to boot up a public minecraft server to be accessed over the internet (or LAN if that's your thing.)

Note: This is definitely the most insecure option of the three, since you're exposing your local network, and host IP to the public. It's not recommended for public Minecraft servers, but since it's just me and a couple of friends, this is the option I'm going to go with.

---

## Step 2: Download Javas
