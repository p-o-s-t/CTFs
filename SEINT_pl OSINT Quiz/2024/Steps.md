The 2024 OSINT Quiz by [@SEINT_pl](https://github.com/seintpl) and [@sector035](https://sector035.nl/) can be found [here](https://github.com/seintpl/osintquiz/tree/main/2024)!  

Verification of completion: MD5 of final step image file == "9ac14a4bf0e10ea9fd3537ad61359252"

<h1>WARNING: THERE BE SPOILERS AHEAD!  TURN AWAY IF YOU WANT TO DO THE QUIZ YOURSELF!</h1>

## Step 1
>Beep! - another email arrived. A bargain sale again, a meeting reminder or maybe this time someone wanted to write to me personally about something more interesting than lower prices, new offers or another time wasting things? I looked at the screen and noticed that the new mail stayed in the Inbox folder. That could mean only two things: either my filters were failing or the message was really meant for me to read. It was the latter this time which made me smile. And when I looked at the Sender’s name, my eyes opened even more. It was an email from my friend, who’s adventures I’ve been tracking a couple of times. My friend didn’t write normal emails, oh no, but liked riddles and non-direct stories. I couldn’t do anything else but to start reading. If you would like to read and follow this adventure with me, here’s the tale:

>And so the adventure ends. We have just arrived at the airport after a long and interesting journey. I took a picture here. They say you never really appreciate the adventure until it’s over. The last flight of this journey went smoothly and lasted exactly as long as it was scheduled. I personally appreciate when the airlines go by the schedule, but this time I had to stop watching a movie I always wanted to see when we were landing, I started watching it as soon as we started the flight and hoped that it would last a few minutes longer, but this time it didn’t and I will have to find out what was the meaning of ‘Rosebud’ later. And I was so close to finding it out on the plane. But this wasn’t the only plot twist during the journey, no! There were more of them. Do you want to hear them? If so, the next story is guarded by the name of the city we were flying from. Can you tell what the name is?

---

Findings from text:
- Citizen Kane is the movie.  It is between 114 minutes - 119 minutes, depending on source. 
- Flight should be approx. 110 minutes

![step1](https://github.com/user-attachments/assets/96f98ce4-1189-4ddc-82e4-f8ca4292a33d)

Findings from the attached photo:  
* **Herrer** is an word in a currently unknown language that is equivalent to the word **Gentlemen** in English 
* The airport has a sign design (that's a fun phrase) with white and yellow text, bright yellow numbers, and an all black background
* Using `exiftool` on the image, we see that the picture was taken at 1308 on 07 August 2024.  UTC time is assumed, since no fields with a timezone offset are observed.
* The gate used for arrival is across from a bathroom.

The first thing I try is to identify the language that the word **Herrer** comes from by using the translate language feature in DuckDuckGo.  It detects the language of **Norwegian**, so I'm off to look at major airports in the country of Norway.  

I initially start with the airport in Oslo (IATA: OSL, ICAO: ENGM).  Checking out some photos through Google Maps, I see the same sign design used throughout the airport, as well as seeing as there are different terminals or concourses with the naming convention of \<English Letter\>\<Number\>, like B8!  

But additional searching looks like all B# gates are for domestic flights.  And looking at the layout of terminal B, I don't see a bathroom across the way from the exit of B7, where our mysterious traveler most likely stepped out from.

Okay, so I pivot to look at other airports in Norway, but they don't seem to have any gates that start with the English letter 'B'.  They all have the same sign design, except for the letters, but nothing is lining up with the picture for Step 1.

I give up for a few days and eventually come back, starting all over with identifying if there's another language that might be detected for **Herrer**.  This time, I use Google Translate and that gives me the language **Danish**.  Okay, a new start! 

Trying again to look at the major airports, I start with Copenhagen (This is also when I find out that Norway's airports aren't the only one that use that design scheme for their signs... Well dang.  and that the only B8 gate that I could find for major airports in Norway is for domestic flights.  It could be Tromso, as the flight time is pretty close, but the layout doesn't match up very well.  

Back to step 1: what other languages does 'Herrer' possibly translate to?  Danish.  Okay, let's check for the major airport in Denmark's capital, Copenhagen (IATA: CPH, ICAO: EKCH).  
The airport is pretty big and it does have a Gate B8, which is right next to a [bathroom](https://www.ifly.com/airports/copenhagen-CPH-airport/terminal-map/Concourse-B-map).  Checking Google Maps, we have some photos that help to [confirm](https://www.google.com/maps/@55.627435,12.6453089,3a,37.3y,18.86h,85.81t/data=!3m10!1e1!3m8!1sAF1QipOgej12durY_4k3jUnLtsFtdoLGvmq78C0TUxag!2e10!6shttps:%2F%2Flh3.googleusercontent.com%2Fp%2FAF1QipOgej12durY_4k3jUnLtsFtdoLGvmq78C0TUxag%3Dw900-h600-k-no-pi4.191961347110123-ya8.400156654649175-ro0-fo100!7i7200!8i3600!9m2!1b1!2i29?entry=ttu&g_ep=EgoyMDI1MDIxMi4wIKXMDSoASAFQAw%3D%3D) this.

![Pasted image 20250215160041](https://github.com/user-attachments/assets/23bcef9c-62dd-4019-85de-3b530f2a92af)

There's also the similarities in the design of the terminal:

![Pasted image 20250215160800](https://github.com/user-attachments/assets/5ff1c8d4-0e60-4b7c-b80c-d63e24db40a4)

These gates appear to be used by Aegan Airlines, based on the overhead imagery of the airport:
![Pasted image 20250215162617](https://github.com/user-attachments/assets/5096e160-b839-4e20-82b7-04ab63fc9f33)

But the only destination seems appears to be from Athens, whose flight time is over 3 hours.  

There are some other aircraft further down, which have a red tail engines rather engines along the wings.

![Pasted image 20250215163259](https://github.com/user-attachments/assets/51b66d2a-f397-4bb6-81fb-71bd54b15dba)

A Reverse image search shows these are in the CRJ700 series of planes, but it's hard to make out the airline, so I instead I try something different by looking at arrivals to Copenhagen on Wednesdays (that was the day of the week for 07 August 2024) that are slated to arrive at 1300.  

![Pasted image 20250215164649](https://github.com/user-attachments/assets/847bee4b-2495-4bad-afea-b9e984492918)

Another cross reference check using [FlightAware](https://www.flightaware.com/live/findflight?origin=LFPG&destination=EKCH) shows that the slated flight time is 110 minutes hours, which matches back with the run time of the movie **Citizen Kane**.  I think our point of origin is **Paris**!

MD5 of Paris == "ccbee73cd81c7f42405e1920409247ec" and that unlocks our next step!

Total time to solve: lol, too long!  I think about 4 hours over the course of a few days?

## Step 2
> Yes, we were coming back from Paris, but it is not the city of love that we stayed in. Our previous stop, during our journey, was a little island, which you will find, if you head southwest. This island was the witness of a British steamship being wrecked 130 years ago (the exact day of the anniversary was in September 2024, but what are a few months when you’re talking about more than a hundred years). The story ended well, but it was frightening. I wish that we could spend more of our summer days there. Did you know that a couple of years ago they found a new species of snail on that island? That’s amazing! Can you find its latin name?

The Latin name of the snail, written in lowercase, without a space (like this: snailusrapidus), is the answer. Turn the words into an MD5 hash to get to the next step.

---
No image this time!  Just some cryptic text about a... snail?  An island snail?

Findings from text:
- Looking for an island
- Island is southwest of Paris
- A British steamship wrecked nearby on some day in September 1894, but with a happy ending?
- The answer is a new species of snail on said island

An initial search for `british steamship wreck 1894 september` leads me to this [page](https://bandcstaffregister.com/page2069.html) about the ship DUNOTTAR CASTLE.  It's said that it actually did run aground on the Eddystone rocks, but was not a complete wreck and continued sailing for many more years.  

![Pasted image 20250215170504](https://github.com/user-attachments/assets/ca2fdfdf-b870-4364-9ce1-db7fa0d863aa)

But that's not southwest of Paris...  Let's try broadening our search a little more by looking at the results, one of which is a [Wikipedia article about wrecks in the year 1894](https://en.wikipedia.org/wiki/List_of_shipwrecks_in_1894).  Looking through the list, going by country of ownership, I see another candidate that may match called the [***SS DORUNDA***](https://web.archive.org/web/20110721101409/http://www.plimsoll.org/images/16619_tcm4-251097.pdf), that received serious damage near the Estellas Rocks near Barlings, Portugal on the 27th of September, 1894.

Now, I'm no geographic wizard, but I'm pretty sure that's Southwest of Paris.

In the report for the wrecking of the SS Dorunda, there is a mention of "the Burlings", which matches with this [Wikipedia article](https://en.wikipedia.org/wiki/Berlengas) that states

> These islands were traditionally known to British mariners as "the Burlings"

Which I completely misread initially as "the Berlings" at first, but is in reality the **Berlengas**.  Doing a quick text search for "snail" on the Wikipedia article for Berlengas leads me to another article about [***Oestophora***](https://en.wikipedia.org/wiki/Oestophora), which has a full Latin name of "[Oestophora barrelsi](https://natuurtijdschriften.nl/pub/644134/BAST2015079001006.pdf)" 

MD5 of oestophorabarrelsi == "7bf817ca3f80cb9251b98b4ddf7be989"

```ad-note
Barrelsi is the old Dutch name for this archipelago ("The Barrels").
```

Total time to solve: 17 mins!  Let's hope I can keep this pace!

## Step 3
> My friend hasn't written since the last time we spoke about snails on the Portuguese coast. I was a little concerned, so I wrote a quick message and asked if there was some kind of new adventure going on. The reply came almost instantly, but… As always, it wasn’t a normal message. It was just a photo with some hills and woods. So again, to know where my friend was travelling, I had to do a little search. Will you help me? Along with the photo, there was also a question - “what were the words written there, just right next to the snake, in the year of that animal?”

---

![step3](https://github.com/user-attachments/assets/567de27c-7b37-4db6-ab40-998c8bbe2198)

Findings from picture:
- Flag in the bottom left has some form of Asian characters.  East Asia, maybe Southeast Asia?  

Finding from text:
- We're possibly looking for some famous words written at this location
- '*Next to the snake*' may indicate some kind of statue?
- The year they were written was a Year of the Snake?  Year of the Snake occurs every 12 years, with the newest one starting on 19 Jan 2025.  So I'll use that later on to confirm some info.  

 Using translate.google.com and drawing some of the characters on the flag, I get some hits for 'Chinese (Simplified)' like  奉  (Feng) and  平  (flat), but i'm unable to get any of the other characters recognized.  I struggled with this for quite some time, but decided I was getting nowhere fast and revisited the instructions and the hints.

One of the hints stuck out in particular, talking about which way the winds blows.

> The flag position changes while the wind blows. Sometimes it blows from one direction, and sometimes it blows from the opposite side.

I didn't comprehend what this meant the first time, but this time I decided to think about it more literally.  How would the flag face if the wind was blowing in the opposite direction?  Perhaps the orientation of the characters would change too.  

![step3r](https://github.com/user-attachments/assets/9750f2dc-cb7c-446e-81b4-38f7bf977b93)

So with that in mind, I did a horizontal flip of the image and then take a separate screenshot of the flag.  Putting this through Google Translate now delivers an output of [**Nachikatsuura**](https://en.wikipedia.org/wiki/Nachikatsuura)  Looks promising!

Still, this town is a lot of area to cover, so before just trying to go meter by meter in locating where the picture is taken, I do a search for 'things to do in nachikatsuura', bringing me to a [TripAdvisor page](https://www.tripadvisor.com/Attractions-g1121355-Activities-Nachikatsuura_cho_Higashimuro_gun_Wakayama_Prefecture_Kinki.html) with top items, with something called **Kumano Kodo** near the top.

Back to Google Maps, I look for Kumano Kodo shrine and get a hit for **Kumano-Nachi Taisha Grand Shrine**.  Moving around a bit, I confirm I'm in the right location by matching up the shape of the mountains from the original picture with one from [Google Maps](https://www.google.com/maps/@33.6694029,135.8904899,3a,90y,31.96h,89.84t/data=!3m7!1e1!3m5!1skD45tesmHuuq3HDY8b3HxA!2e0!6shttps:%2F%2Fstreetviewpixels-pa.googleapis.com%2Fv1%2Fthumbnail%3Fcb_client%3Dmaps_sv.tactile%26w%3D900%26h%3D600%26pitch%3D0.16243902716752245%26panoid%3DkD45tesmHuuq3HDY8b3HxA%26yaw%3D31.958378497404073!7i13312!8i6656?entry=ttu&g_ep=EgoyMDI1MDIxMi4wIKXMDSoASAFQAw%3D%3D):

![Pasted image 20250216113141](https://github.com/user-attachments/assets/300d71f9-e285-4aa6-97d3-2f18ee6549a9)

"Walking" up the path to the main area of the shrine, I come across this sign that displays a rooster:

![year_of_rooster](https://github.com/user-attachments/assets/3decb04d-f015-45b6-b109-4098dbd88a27)

I notice that there are some other dates available, so I select the entry for May 2013, which now displays a snake in the same spot where the rooster was in 2016.  This matches up with the 12-year rotation for the Year of the Snake (2025 - 12 = 2013).  

![year_of_snake](https://github.com/user-attachments/assets/dc8e2780-e0c7-4999-ab9d-91f74df50e4d)

![Pasted image 20250216113735](https://github.com/user-attachments/assets/fe41ec56-47cc-4d04-949c-490a75128953)

MD5 of 'goodluck' == "14ed1a22176d3805f01deeab4c7aae03"

And it must be my lucky year, cause that was the right answer!

Total Time to solve (including times with incredibly poor signal strength on a plane): 3 hours

## Step 4
> The music was playing in the background. The kind of music that gives you energy while looking for all these places all over the world. The lyrics were in Spanish, but as I could understand some basic words, they were saying: “Let's go on a trip to look for magical sounds”. What a wonderful phrase for our quest! Let’s look for the magical sounds in the country the song tells about. This country's largest city’s website has a long history, as well as the telephone number for their office. The number has changed over the years, but can you find the telephone number of the municipality from 2010? 

No picture this time, but some kick ass lyrics:
- Lyrics in Spanish
- "Let's go on a trip to look for magical sounds” is about a certain country
- Country's largest city has a site with a phone number
- Get the number for the municipality from 2010

Using [Google Translate](https://translate.google.com) for the phrase, I get the result of "**Vamos de viaje para buscar sonidos mágicos.**"  I confirm this with the translate function with DuckDuckGo and get the same phrase.

Using literal strings for the phrase, I get hits for a song called [**Ecuador** by *Sash! feat. Rodriguez*](https://www.youtube.com/watch?v=f2sO9yLQhP4).  

I pivot off the name of the song- while listening to this absolute BANGER of a song :dancing_wizard_emoji:- to find out the name of the largest city in Ecuador through DuckDuckGo.  This time, I get an AI assist response that tells me that **Guayaquil** is the largest city in that country.

![Pasted image 20250216222851](https://github.com/user-attachments/assets/1b6deb99-b571-4c1d-828c-3eb38ca229a0)

Looking at the citation from Wikipedia, I eventually find that this city is in the municipality of [**Guayaquil Canton**](https://en.wikipedia.org/wiki/Guayaquil_Canton).  On this article, the Website for this municipality is listed as https://www.guayaquil.gob.ec/.

But we need what the site looked like all the way back in the year of 2010, so it's off to the Wayback Machine!  The site is pasted in and we get 787 hits (at time of this writing) for the website.  You can see those results [here](https://web.archive.org/web/20100601000000*/https://www.guayaquil.gob.ec/).  The earliest available snapshot of the website is from 16 October 2010.  

I would paste a screenshot of the site here, but it's pretty basic with hyperlinked text on a white background and a small insert of a Google search bar.  Scrolling down to the bottom of the page, which typically contains the contact information related to the web site, I come across an entry for **Teléfono: 259-9100**

MD5 of 259-9100 == "56c5134c968742ba585d42e1911c9eed"

I wonder if that's the same number where I can reach Jenny...

Total time to solve: 30 minutes, because I was eating dinner at the same time and had to deal with a very cute dog giving me those puppy eyes while begging for some of my food.  *And* I also got distracted by the song from this challenge and had to bust out some dance moves around my cats and spouse for a few minutes.

## Step 5
> That was a beautiful view of Ecuador and its rainforests. But sometimes you travel through not only a forest, but a real jungle. This time it is a city jungle. Can you guess what place this is? The brown building with the car logo in the back was repainted lately and now it has a new sign on the wall.   

![Pasted image 20250216224502](https://github.com/user-attachments/assets/1c396372-e869-4adf-934f-e1368a029be8)

Findings from the picture:
- Vehicles are driving on left side of the road
- Mitsubishi symbol in the middle of the picture on a building with brown paint
- Red ***JRC*** with a red boxed border on a sign
- A business that has a baby(?) with a learning cap(?) on a sign
- What looks like a sports field?
- Asian style characters, suggesting East Asia

Findings from the text: not much!  Most of the info needed for this one is in the photo this time.

Well, first things first, let's throw this bad boy into [Google Translate](https://translate.google.com) and see what we can glean from it.

![Pasted image 20250216225138](https://github.com/user-attachments/assets/8a0b30dd-d63b-4920-9669-a36c367b4cbf)

Searching for "**Mitsubishi Electric Gymnasium**" brings me to Nagasaki, Japan.  It has a hit for a location and a quick look through the [photos](https://www.google.com/maps/place/Mitsubishi+Electric+Gymnasium/@32.75273,129.8645792,3a,75y,90t/data=!3m11!1e2!3m9!1sAF1QipMRtSWx14emZ1Vin4Ij0iE0FThAH5Z-WCDWIE3k!2e10!3e12!6shttps:%2F%2Flh5.googleusercontent.com%2Fp%2FAF1QipMRtSWx14emZ1Vin4Ij0iE0FThAH5Z-WCDWIE3k%3Dw203-h135-k-no!7i8256!8i5504!9m2!1b1!2i29!4m16!1m8!3m7!1s0x35155324736c8737:0x63f93d9729130bcf!2sMitsubishi+Electric+Gymnasium!8m2!3d32.7526889!4d129.8646017!10e5!16s%2Fg%2F1wn31f5h!3m6!1s0x35155324736c8737:0x63f93d9729130bcf!8m2!3d32.7526889!4d129.8646017!10e5!16s%2Fg%2F1wn31f5h?entry=ttu&g_ep=EgoyMDI1MDIxMi4wIKXMDSoJLDEwMjExNDU1SAFQAw%3D%3D) helps to confirm I'm looking at the same place.

![Pasted image 20250216225504](https://github.com/user-attachments/assets/3e2a1e31-2bea-4476-8eff-204a5601e171)

Using Google Street View to ~~case~~ check out the building for a few minutes, I eventually come a sign that has some writing on the bottom of it, along with what appears to be a new owner!

![Pasted image 20250216225919](https://github.com/user-attachments/assets/e86f5715-ef77-43f2-9b67-eb1eeec51c12)

MD5 of "2005nagasaki" == "cbcec30543dd08f3959ac3ada3df04ab"

Total time to solve: 11 minutes

## Step 6
> But let's not hang around too long in city jungles, because there is so much more to explore! The next stop seems to be a country that is known for its animals, especially a collection of unique primates. There are also five bird families unique to this country, and roaming the lands once, was a very special big bird. The latin name of this bird will give you the answer to unlock the next question. 

Findings from text:
- Country with unique primates
- Country with with five unique bird families
- Looking for the Latin Name of a VERY special BIG bird.

Having ***NO*** idea how to write this query, I fall back to using ChatGPT this time around and using the prompt `What country has five unique bird families within it?`  The response I get is:

```
The country with five unique bird families is **New Zealand**. It is known for its distinct avian diversity, with many birds that are found nowhere else in the world. Some of the notable bird families that are unique to New Zealand include:

1. **Apterygidae** (Kiwis) - Kiwis are flightless birds that are iconic symbols of New Zealand.
2. **Cacatuidae** (Cockatoos) - While some species exist elsewhere, New Zealand is home to a few distinctive species.
3. **Eremophilidae** (Rock wrens) - A family of small, terrestrial birds that are found in mountainous regions of New Zealand.
4. **Mochloridae** (New Zealand rockhopper penguins) - A family of penguins native to the country’s subantarctic islands.
5. **Callaeidae** (New Zealand wrens) - Unique to the region, these species are often found in forested areas.

New Zealand's isolation has led to the evolution of many bird species that are distinct from those found elsewhere in the world.
```

But to verify before going any further, I follow this response with the prompt of `Does New Zealand also have a unique collection of primates?`, in which I receive a negative response.  Okay, looks like New Zealand isn't the right location to look at, so let's try backing up and looking for a country with unique primates.

A search for "country with collection of unique primates" in DuckDuckGo gives me another option for an Assisted answer, giving me the response of

```
Madagascar is known for its collection of unique primates, particularly lemurs, which are found nowhere else in the world. The country's isolation has led to a high level of endemism among its primate species.
```

Like King Julian, it's time to *move it move it* to this new pivot and follow up a little more to see if Madagascar is the right country.

Searching for "families of birds in madagascar" gives me the [List of Birds of Madagascar](https://en.wikipedia.org/wiki/List_of_birds_of_Madagascar).  Reading through this article, my eye catches the section titled **Greater Elephant Birds**, which are also listed as extinct.  _Aepyornis maximus_ is listed as "possibly the largest bird to have lived".  Sounds like this is our bird!  Or rather, it is the bird that was but is no more!

MD5 of aepyornismaximus == "9b4818696a622641ecce3f57183edf01"

Total time to solve: 12 minutes

## Step 7
>I just remembered something interesting, while I was thinking about my next location, let's see if you can figure it out... When the steamship got stuck near Berlengas, Portugal, another type of transport was very dear to some of my ancestors. I might still have some old photographs about their journey somewhere... But I digress! What I wanted to let you know, is that for 94 years, with some small breaks, this city was very important transport wise! After 94 years, it was not a part of this whole adventure anymore. The only thing keeping its memories are the buildings where the adventure used to end. The architect who designed the building was actually sent by the newly formed German empire for study, but he became the man who created this historically important building. 

Findings from text:
- Event that covered 94 years in all, but more than likely occurred over a period greater than 94 years based on the "small breaks" comment
- Important city for transportation
- Adventure
- Buildings are still kept around even though the adventure isn't conducted any more.
- Newly formed German empire

This sounds like it's talking about the contest of circumnavigating the world by any means, kind of like the Jules Verne novel *Around the World in Eighty Days*.  But I've got no idea on what the other important type of transport would be.

A quick search for 'german empire' shows that it formed some time in 1871, according to Britannica.  So looking for someone who was sent after that time.

I took a few days off because I was on vacation on a tropical island and that was just a *bit* more exciting than this CTF!  Hopefully the break will help me figure this step out.  

After thinking it over for a bit, nothing comes to mind on a specific type of transportation.  I check over the hint for this step again and nothing really sticks out to me.  I revisit the original text and this time, the line of "I might still have some old photographs about their journey somewhere..." makes me think that there may be some clues back in @SEINT_pl's Twitter feed.  But I can't access that right now, so I'll try something else.

I look up the timeframe for the German Empire, which looks to have lasted between 1871 - 1918.  And for the next few hours, I messed around with some prompts to try some other candidates which may fit the example.

- palazzodandolo
- hansvonderlinde
- lisbontrainstation
- sirkecirailwaystation
- tostedtstation
- sirkeciterminal
- istanbulrailwaystation

Finally, I thought to try the architect himself:

MD5 of "augustjasmund" ==" 7cf20e31fd46d3c6100f48537254aeb1"

That one was tough.  Would have never gotten it without the help of ChatGPT.

Total time to solve: 5 hours over a week.

## Step 8
> I really love nature, animals, old architecture, but to be honest, I can also enjoy some European art! During my latest travels, I also visited a famous museum, where I was fortunate to view some lovely paintings, which were all on display, and took some awesome photos. But somehow, after I managed to create a collage of some of the paintings, I lost the original ones! Can you help me find the original painters? Just the first two letters of their real first names are enough for me to be reminded. Just collect the eight characters, convert them to lower case, put them in alphabetical order, and hash them. So let's say all of them were painted by Vincent van Gogh, the first two letters are "vi", and in alphabetical order, all eight would be: "iiiivvvv". Got it? Off you go!

![step8](https://github.com/user-attachments/assets/b00e8875-9334-4402-9a73-54abc06c56dd)

Findings from text:
- European art
- All of the paintings are in the same museum
- Need the first 2 letters of their real first names then combine, then sort by English alphabet index (A-> 1, Z-> 26)

Findings from picture:
* Not much to go off here.  Reverse image search is going to be my go-to for this.

I'm going to try using Bing for this step, just to change things up a bit and see if it's still a good tool for performing reverse image searches.

By focusing on each of the areas, I'm able to get some hits:
- In the bottom right, I get hit for a painting by Rembrandt (re)
- In the top left, I get a hit for [*Ginevra de' Benci* by Leonardo da Vinci](https://www.nga.gov/collection/art-object-page.50724.html) (le)
- The bottom left is inconclusive as of yet, lots of red haired women with curls and lips.  Who would've guessed.
- And finally, in the top right, I get a hit for [_Portrait of Marchesa Brigida Spinola-Doria_ by Sir Peter Paul Rubens](https://www.nga.gov/collection/art-object-page.46159.html) (pe)

Both of the identified paintings are located in the [National Gallery of Art](https://www.nga.gov/).  Which is good, because I'm unable to find good matches for the bottom parts.  I even tried using Google Image search and didn't get anything new.

Instead I go all collections of paintings, starting with the Baroque period filter.  I get lucky on page 11 of 14 to find  [_Portrait of a Lady_](https://www.nga.gov/collection/art-object-page.121137.html) by Nicolaes Maes (ni).  That's 3 out of 4!

The last image in the bottom left required me to use Yandex, which to this day still has a legitimately good reverse image search.  I get some hits for a name of "Slvator Mundi".  Looking this up on the National Gallery of Art site gets me this painting, [*Salvator Mundi* by Correggio](https://www.nga.gov/collection/art-object-page.46167.html) (co).  

Okay, time to verify everyone's given name.
- Leonardo da Vinci was also known as Leonardo di ser Piero da Vinci.  So we got "le"
- Sir Peter Paul Rubnes had no changes.  We got a "pe"
- Nicolaes Maes had no changes.  We have a "ni"
- Corregio was usually just referred to as Corregio, but his full name was Antonio Allegri da Correggio. The last one is an "an"

Using CyberChef I use the Sort operator to do all the work for me so my brain doesn't have to do any more thinking on Step 8. 

`https://gchq.github.io/CyberChef/#recipe=Sort('Nothing%20(separate%20chars)',false,'Alphabetical%20(case%20sensitive)')&input=bGVwZW5pYW4`

MD5 of "aeeilnnp" == "ea69316800f41dee1af6ff3dd46c2150"

Total time to solve: 96 minutes.  

## Step 9
> It’s December now and we are all back home from our adventures around the world. How did I know that even my friends are home? They sent me an invitation to meet for a nice winter cup of hot coffee. The meeting place was of course not sent directly. That would be too easy. Instead, they sent me a short message, which contained just a couple of words and said that our meeting point would be the place: only.sector.deduced. Where can that be? Can you help me? 

Oh a classic.  I actually just used this recently in a challenge for my local cybersecurity community.  The meeting point uses three words, which in turn is used for the very cool website, [what3words](https://what3words.com/only.sector.deduced).  

![Pasted image 20250224132418](https://github.com/user-attachments/assets/cecf619f-5911-4a13-a655-642ed74af657)

That gets us to Wola, Mazovia, which is in the city of Warsaw, Poland.  Going off some of the links in the google maps entry for Park Place 3, it looks like this building was built in 2017, perhaps 2018.

MD5 of "2017warsaw" == "ab85ff52c6675832dbb57a315d476c43"

Total time to complete: 9 minutes

## Step 10
OMG THERE'S MORE!?!?!?!

```
  .oooooo.                                                           .               oooo                .    o8o                                 .o. 
 d8P'  `Y8b                                                        .o8               `888              .o8    `"'                                 888 
888           .ooooo.  ooo. .oo.    .oooooooo oooo d8b  .oooo.   .o888oo oooo  oooo   888   .oooo.   .o888oo oooo   .ooooo.  ooo. .oo.    .oooo.o 888 
888          d88' `88b `888P"Y88b  888' `88b  `888""8P `P  )88b    888   `888  `888   888  `P  )88b    888   `888  d88' `88b `888P"Y88b  d88(  "8 Y8P 
888          888   888  888   888  888   888   888      .oP"888    888    888   888   888   .oP"888    888    888  888   888  888   888  `"Y88b.  `8' 
`88b    ooo  888   888  888   888  `88bod8P'   888     d8(  888    888 .  888   888   888  d8(  888    888 .  888  888   888  888   888  o.  )88b .o. 
 `Y8bood8P'  `Y8bod8P' o888o o888o `8oooooo.  d888b    `Y888""8o   "888"  `V88V"V8P' o888o `Y888""8o   "888" o888o `Y8bod8P' o888o o888o 8""888P' Y8P 
                                   d"     YD                                                                                                          
                                   "Y88888P'                                                                                                          
                                                                                                                                                     
CONGRATULATIONS!
```
No, that's it!  We did it everyone!  🏅

![image](https://github.com/user-attachments/assets/6014cb25-f0eb-4812-b8ad-75b8864c932f)

And of course **Step 11** continues the tradition of a fantastic punny joke (which some may call a Dad Joke).  But I'll leave that to you to discover.  😸

## Closing Notes
These are always fun and great way to stretch out my brain muscles.  I really appreciate the work and effort that went into this.  Looking forward to starting a little earlier next year.

To wrap things up, here's my joke: 

Why did the map always get invited to parties?
Because it _knew the way_ to have a good time! 
