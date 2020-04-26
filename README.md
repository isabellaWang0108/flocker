# Flocker
An application which helps solo travelers meet new people, based on common interests.

Challenge :  How might we improve the travel experience for solo travelers

Deployed on Heroku: [deployed link](https://stormy-caverns-59086.herokuapp.com/)

My core duties : 
*  Infrastructure design
*  Frontend Component
*  Algorithm

## Video demo
(click on image to watch the video)

[![Recorded demo](https://wangx733.github.io/flocker/images/logo.jpg)](https://youtu.be/flJYcaGrT6k)

## Value Proposition
In this project, we did both qualitative and quantitative user research on the pain points of finding travel partners. We interviewed 8 people age from 20s to 40s. And they shared a common concern about compatibility when it comes to travel partner.

![Personas](https://wangx733.github.io/dearTime/images/persona.jpg)


## Tech Stack
Here are the technologies we used:

 * language: HTML, CSS, Javascript
 * Heroku Plugins: Cloudinary, JawsDBMySQL
 * Libraries: pretty checkbox, jQuery
 
![Tech stack](https://wangx733.github.io/dearTime/images/tackstack.svg)

## Data Model
![Data model](https://wangx733.github.io/dearTime/images/dataModel.png)

## Matching Algorithm
For the design of matching people, we decided to go with the theory that the more people are alike, the better they get alone with each other Thus, we just check every single options in the database, one same item = 1 point. The more common answers the higher the score. Then, we just display the users in order of high to low base on the score.

```javascript
   // the list of people
      var myjson = [];
      var highestScore = 0;

      var me = result[result.length - 1];
      for (var i = 0; i < result.length - 1; i++) {
        var count = 0;
        var people = result[i];
        if (me.dest1 == people.dest1 || me.dest1 == people.dest2 || me.dest1 == people.dest3) {
          count++;
        };
        if (me.dest2 == people.dest1 || me.dest2 == people.dest2 || me.dest2 == people.dest3) {
          count++;
        };
        if (me.dest3 == people.dest1 || me.dest3 == people.dest2 || me.dest3 == people.dest3) {
          count++;
        };

        if (me.prefered_trip == people.prefered_trip) {
          count++;
        }
        // check interest
        var myintrests = me.intrests.split(',');
        var peopleintrests = people.intrests.split(',');
        var numberOfIntrest = 0;
        if (numberOfIntrest !== myintrests.length - 1) {
          for (j = 0; j < myintrests.length; j++) {
            if (myintrests[numberOfIntrest] == peopleintrests[j]) {
              count++;
            }
          }
          numberOfIntrest++;
        }

        // check language
        var mylanguage = me.language.split(',');
        var peoplelanguage = people.language.split(',');
        var numberOflanguage = 0;
        if (numberOflanguage !== mylanguage.length - 1) {
          for (a = 0; a < mylanguage.length; a++) {
            if (mylanguage[numberOflanguage] == peoplelanguage[a]) {
              count++;
            }
          }
          numberOflanguage++;
        }

        // check diet
        var mydiet = me.diet.split(',');
        var peoplediet = people.diet.split(',');
        var numberOfdiet = 0;
        if (numberOfdiet !== mydiet.length - 1) {
          for (b = 0; b < mydiet.length; b++) {
            if (mydiet[numberOfdiet] == peoplediet[b]) {
              count++;
            }
          }
          numberOfdiet++;
        }


        if (count > highestScore) {
          highestScore = count;
          myjson.unshift(result[i]);
        } else {
          myjson.push(result[i]);
          console.log("you are small");
        }
      }
      res.json(myjson);
    });
  });

```

## User flow

![user flow](https://wangx733.github.io/dearTime/images/workflow.png)

## Future direction
  * Membership module
  * Ai based searching function
