---
layout: project
title: OSRSBOX | An OSRS Item Database Available via a RESTful API
project_name: OSRSBox Database
project_desc: A database of Old School Runescape (OSRS) items in JSON format with accompanying icon images in PNG format
redirect_from:
  - osrs-database
---

This project is a database of Old School Runescape (OSRS) items in JSON format with accompanying icon images in PNG format. The goal of the project is to provide a JSON object and PNG image for **every item in OSRS**. In addition, the metadata for each item is extensive including as many useful properties as possible.

The repository that accompanies this project provides public access to JSON formatted metadata about every OSRS item in the game; for example, whether an item is tradeable, stackable, or equipable or if the item is members only, or a quest item. For any equipable item, there is metadata about combat stats the item has; for example, what slash attack bonus, magic defence bonus or prayer bonus an item provides. Furthermore, high and low alchemy values are provided. Lastly, each item has a corresponding item icon in PNG format. 

**NOTE:** This project has not been updated since December 26th, 2017. I am currently rewriting the code to automatically parse the OSRS cache, combined with the tools used to parse the OSRS Wikia. This will hopefully streamline the update process in the future.

## JSON structured data

The osrsbox-db stores information about OSRS items in separate JSON files. For example, [this link](https://www.osrsbox.com/osrsbox-db/items-json/12453.json) provides direct access to the `12453.json` file, which holds metadata about the Black wizard hat (g) item. In OSRS, the ID number `12453` is unique to the Black wizard hat (g). This is why the item IS is utilised in the database for fetching all item information. 

But what is actually contained in these JSON files? Well, it is a collection of metadata (information) about the specific item. There are two main categories of metadata about an item: 

- Item properties
- Item stats

### Item Properties

All items have properties; for example, the item's weight and the items high alchemy value. All item properties are listed below for reference, including the data type (e.g., string, integer, float) for each property and a description of the property.

{: .table .table-striped .table-sm}
| Property     | Data type   | Description                              |
| ------------ | ------------| ---------------------------------------- |
| id           | integer     | Unique OSRS item ID number               |
| name         | string      | Name of the item                         |
| release_date | string      | Date the item was released               |
| members_only | boolean     | If the item is a members only item or not |
| quest_item   | boolean     | If the item is a quest item or not       |
| tradeable    | boolean     | If the item is tradeable or not          |
| equipable    | boolean     | If the item is equipable or not          |
| stackable    | boolean     | If the item is stackable or not          |
| high_alch    | integer     | The high alchemy value of the item       |
| low_alch     | integer     | The low alchemy value of the item        |
| buy_limit    | integer     | The Grand Exchange buy limit of the item |
| weight       | float       | The weight (in kilograms) of the item    |
| examine      | string      | The examine text of the item             |
| url          | string      | OSRS Wikia URL link                      |

### Item Stats

If an item is equipable it will have additional metadata about the combat bonuses that it provides; for example, the melee strength bonus the Dragon dagger item provides. The following table specifies the 14 different stats an item has. Please note that all item stats are stored as an integer data type.

{: .table .table-striped .table-sm}
| Property        | Data type | Description                           |
| --------------- | --------- | ------------------------------------- |
| attack_stab     | integer   | The stab attack bonus of the item     |
| attack_slash    | integer   | The slash attack bonus of the item    |
| attack_crush    | integer   | The crush attack bonus of the item    |
| attack_magic    | integer   | The magic attack bonus of the item    |
| attack_ranged   | integer   | The ranged attack bonus of the item   |
| defence_stab    | integer   | The stab defence bonus of the item    |
| defence_slash   | integer   | The slash defence bonus of the item   |
| defence_crush   | integer   | The crush defence bonus of the item   |
| defence_magic   | integer   | The magic defence bonus of the item   |
| defence_ranged  | integer   | The ranged defence bonus of the item  |
| melee_strength  | integer   | The melee strength bonus of the item  |
| ranged_strength | integer   | The ranged strength bonus of the item |
| magic_damage    | integer   | The magic damage bonus of the item    |
| prayer          | integer   | The prayer bonus of the item          |

### JSON Structure

So what does this JSON object actually look like? Well, listed below is an example of a complete JSON object for the Black wizard hat (g). You could just click on [this link](https://www.osrsbox.com/osrsbox-db/items-json/12453.json) to view the raw JSON using the osrsbox-db API.

{% highlight json %}
{
  "id": 12453,
  "name": "Black wizard hat (g)",
  "tradeable": true,
  "stackable": false,
  "notable": true,
  "equipable": true,
  "members": false,
  "weight": 0.4,
  "buy_limit": -1,
  "quest_item": true,
  "release_date": "12 June 2014",
  "cost": 2,
  "lowalch": 0,
  "highalch": 1,
  "examine": "A silly pointed hat, with colourful trim.",
  "url": "http://2007.runescape.wikia.com/wiki/Black_wizard_hat_(g)",
  "bonuses": {
    "magic_damage": 0,
    "defence_stab": 0,
    "defence_magic": 2,
    "ranged_strength": 0,
    "attack_stab": 0,
    "attack_magic": 2,
    "defence_crush": 0,
    "defence_slash": 0,
    "prayer": 0,
    "attack_slash": 0,
    "defence_ranged": 0,
    "attack_crush": 0,
    "melee_strength": 0,
    "attack_ranged": 0
  },
  "item_slot": "head"
}
{% endhighlight %}

## Accessing JSON data about OSRS items

The JSON file for each OSRS item can be directly accessed using unique URLs provide through the `osrsbox.com` website. Technically, this provides the functionality of a RESTful API, but only supports GET requests. That is, you can fetch JSON files using a unique URL but cannot modify any JSON content. Below is a list of URL examples for items in the osrsbox-db:

- [https://www.osrsbox.com/osrsbox-db/items-json/12453.json](https://www.osrsbox.com/osrsbox-db/items-json/12453.json)
- [https://www.osrsbox.com/osrsbox-db/items-json/10.json](https://www.osrsbox.com/osrsbox-db/items-json/10.json)
- [https://www.osrsbox.com/osrsbox-db/items-json/2003.json](https://www.osrsbox.com/osrsbox-db/items-json/2003.json)
- [https://www.osrsbox.com/osrsbox-db/items-json/3097.json](https://www.osrsbox.com/osrsbox-db/items-json/3097.json)
- [https://www.osrsbox.com/osrsbox-db/items-json/3098.json](https://www.osrsbox.com/osrsbox-db/items-json/3098.json)

As displayed by the links above, each item ID is stored in the `osrsbox-db` repository, under the `items-json` folder. 

So how can you get and use these JSON files about OSRS items? It is pretty easy, but really depends on what you are trying to accomplish and what programming language you are using. 

### Accessing JSON Using wget

Take a simple example of downloading a single JSON file. In a Linux system, we could use the `wget` command to download a single JSON file, as illustrated in the example code below:


{% highlight bash %}
wget https://www.osrsbox.com/osrsbox-db/items-json/12453.json
{% endhighlight %}

### Accessing JSON Using Python

Maybe you are interested in downloading a single (or potentially multiple) JSON files about OSRS items and processing the information in a Python program. The short script below downloads the `12453.json` file using Python's urllib library, loads the data as a JSON object and prints the contents to the console. The code is a little messy, primarily due to supporting both Python 2 and 3 (as you can see from the "try" and "except" importing method implemented).

{% highlight python %}
import json

try:
    from urllib.request import urlopen
except ImportError:
    from urllib2 import urlopen

url = ("https://www.osrsbox.com/osrsbox-db/items-json/12453.json")
response = urlopen(url)
data = response.read().decode("utf-8")
json_obj = json.loads(data)
print(data)
{% endhighlight %}

### Accessing JSON Using JavaScript

Finally, let's have a look at JavaScript (specifically jQuery) example to fetch a JSON file from the osrsbox-db and build an HTML element to display in a web page. The example below is a very simple method to download the JSON file using the jQuery getJSON function. Once we get the JSON file, we loop through the JSON entries and print each key and value (e.g., name and Black wizard hat (g)) on it's own line in a div element. If you want to experiment with the code, the code is available in a W3Schools TryIt Editor at [this link](https://www.w3schools.com/code/tryit.asp?filename=FDYXVMBAV85L).

{% highlight html %}
<!DOCTYPE html>
<html>
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
    <script>
      $(document).ready(function(){
          $("button").click(function(){
              $.getJSON("https://www.osrsbox.com/osrsbox-db/items-json/12453.json", function(result){
                  $.each(result, function(i, field){
                      $("div").append(i + " " + field + "<br>");
                  });
              });
          });
      });
    </script>
  </head>
  <body>
    <button>Get JSON data</button>
    <div></div>
  </body>
</html>
{% endhighlight %}

So, if you have read this far, we can fetch OSRS item information using a public API provided by osrsbox-db... But what can we do with this data? The initial reason the osrsbox-db was created was to enable osrsbox-tooltips! Support for elusive items such as the <span class="tooltip osrs-tooltip" id='11806' title='Please wait ...'>[Saradomin godsword]</span>. Please see the [osrsbox-tooltips](https://github.com/osrsbox/osrsbox-tooltips) page for information about the project. However, since then I have used the osrsbox-db project in a variety of other projects whenever information about OSRS items are required.

## Icon images in PNG format

In addition to providing an API to JSON data. This project also provides thumbnail image in the PNG file format. However, not all OSRS items have an accompanying PNG image - usually untradeable items that have no OSRS Wikia page. As an example, see the image below:

Look, it's a ... Black wizard hat (g) ![alt text](https://www.osrsbox.com/osrsbox-db/items-icons/12453.png)

The Item icon images work in a very similar way to the JSON files. Each image is identified and accessed through the `osrsbox.com` website using the unique item ID number. Below is a list of URL examples for items icons in the osrsbox-db:

- [https://www.osrsbox.com/osrsbox-db/items-icons/12453.png](https://www.osrsbox.com/osrsbox-db/items-icons/12453.png)
- [https://www.osrsbox.com/osrsbox-db/items-icons/10.png](https://www.osrsbox.com/osrsbox-db/items-icons/10.png)
- [https://www.osrsbox.com/osrsbox-db/items-icons/2003.png](https://www.osrsbox.com/osrsbox-db/items-icons/2003.png)
- [https://www.osrsbox.com/osrsbox-db/items-icons/3097.png](https://www.osrsbox.com/osrsbox-db/items-icons/3097.png)
- [https://www.osrsbox.com/osrsbox-db/items-icons/3098.png](https://www.osrsbox.com/osrsbox-db/items-icons/3098.png)

As displayed by the links above, each item ID is stored in the `osrsbox-db` repository, under the `items-icon` folder. 

## Project Feedback and Contribution

This is an independent project (thus far). However, I would thoroughly appreciate any feedback regarding the project, especially problems with the inaccuracies of the JSON files and missing items. The best method is to post a Github issue with a feature request, bug or other problem. 
