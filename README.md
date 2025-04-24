# SQLIsland

### 🏝️I use SQLIsland to practice SQL in a fun, interactive way.
Site : [SQL Island](https://sql-island.informatik.uni-kl.de/) | Certificate of Completion : [here](https://sql-island.cs.uni-kl.de/cert.php?id=9b3657f2a1)

---
- **It seems there are a few people living in these villages. How can I see a list of all inhabitants?**
  ```  
    SELECT *
    FROM inhabitant;
  ```     
- **Thank you, Edward! Okay, let's see who is friendly on this island...**
  ```      
    SELECT *
    FROM inhabitant
    WHERE state = 'friendly';
  ```      
- **There is no way around getting a sword for myself. I will now try to find a friendly weaponsmith to forge me one.**
  ```      
    SELECT *
    FROM inhabitant
    WHERE state = 'friendly' AND job = 'weaponsmith';
  ```      
- **Oh, that does not look good. Maybe other friendly smiths can help you out, e.g. a blacksmith.**
  ```      
    SELECT *
    FROM inhabitant
    WHERE state = 'friendly' AND job LIKE '%smith';
  ```      
- **No need to call me stranger! What's my personid?**
   ```     
    SELECT personid
    FROM inhabitant
    WHERE name = 'Stranger';
  ```      
- **I can offer to make you a sword for 150 gold. That's the cheapest you will find! How much gold do you have?**
  ```      
    SELECT gold
    FROM inhabitant
    WHERE name = 'Stranger';
  ```      
- **Damn! No mon, no fun. There has to be another option to earn gold other than going to work. Maybe I could collect ownerless items and sell them! Can I make a list of all items that don't belong to anyone?**
  ```      
    SELECT *
    FROM item
    WHERE owner IS NULL;
  ```   
- **Do you know a trick how to collect all the ownerless items?**
  ```      
    UPDATE item
    SET owner = 20
    WHERE owner IS NULL;
  ```       
- **Now list all of the items I have!**
  ```      
    SELECT *
    FROM item
    WHERE owner = 20;
  ```      
- **Find a friendly inhabitant who is either a dealer or a merchant. Maybe they want to buy some of my items.**
  ```      
    SELECT *
    FROM inhabitant
    WHERE job IN ('dealer', 'merchant') AND state = 'friendly';
  ```      
- **I'd like to get the ring and the teapot. The rest is nothing but scrap. Please give me the two items. My personid is 15.**
  ```      
    UPDATE item
    SET owner = 15
    WHERE item IN ('ring', 'teapot');
  ```      
- **Unfortunately, that's not enough gold to buy a sword. Seems like I do have to work after all. Maybe it's not a bad idea to change my name from Stranger to my real name before I will apply for a job.**
  ```      
    UPDATE inhabitant
    SET name = 'Ezra'
    WHERE name = 'Stranger';
  ```      
- **Since baking is one of my hobbies, why not find a baker who I can work for?**
   ```     
    SELECT *
    FROM inhabitant
    WHERE job = 'baker'
    ORDER BY gold desc;
   ```     
- **Is there a pilot on this island by any chance? He could fly me home.**
  ```     
    SELECT *
    FROM inhabitant
    WHERE job = 'pilot';
  ```      
- **Thanks for the hint! I can use the join to find out the chief's name of the village Onionville.**
  ```      
    SELECT i.name
    FROM village v JOIN inhabitant i
    ON v.chief = i.personid
    WHERE v.name = 'Onionville';
  ```      
- **Hello Ezra, the pilot is held captive by Dirty Dieter in his sister's house. Shall I tell you how many women there are in Onionville? Nah, you can figure it out by yourself!**
  ```      
    SELECT COUNT(*)
    FROM inhabitant
    where gender = 'f' and villageid = '3';
  ```      
- **Oh, only one woman. What's her name?**
  ```      
    SELECT name
    FROM inhabitant
    where gender = 'f' and villageid = '3';
  ```      
- **Oh no, baking bread alone can’t solve my problems. If I continue working and selling items though, I could earn more gold than the worth of gold inventories of all bakers, dealers and merchants together. How much gold is that?**
  ```      
    SELECT SUM(gold)
    FROM inhabitant
    where job IN ('baker', 'dealer', 'merchant');
  ```      
- **Very interesting: For some reason, butchers own the most gold. How much gold do different inhabitants have on average, depending on their state (friendly, ...)**
  ```   
    SELECT state, avg(gold)
    FROM inhabitant
    GROUP BY state
    ORDER BY avg(gold)
  ```
- **Heeeey! Now I'm very angry! What will you do next, Ezra?**
  ```    
    DELETE FROM inhabitant WHERE name = 'Dirty Diane’
  ```    
- **Yeah! Now I release the pilot!**
  ```    
    UPDATE inhabitant
    SET state = 'friendly'
    where job = 'pilot';
  ```    
