##mongoqueries
###requirements

1. Provide a query showing just the names (and nothing else) of the Italian restaurants.
2. Provide a query showing how many Bakeries have a name that start with M.
3. Provide a query showing the zip codes (and _id's) of all restaurants with the word "Ice" in their cuisine.
4. Provide a query showing the street and street number of Chinese restaurants ordered by zip code.
5. Show only the American restaurants in Manhattan.
6. Provide a query showing the restaurants that have been graded exactly 4 times.
7. Provide a query showing only _id, name and 2 grades from each restaurant on Broadway.
8. Provide a query showing the 5 pizza restaurants in the Bronx with the highest score on an evaluation.
9. Provide a query to find all of the restaurants in Brooklynn and list only the 21st-30th results when ordered alphabetically by name.
10. Provide a query that returns all pizza and Italian restaurants in reverse alphabetic order.


###answers
1. db.restaurants.find({cuisine:"Italian"},{name:1, _id:0})
2. db.restaurants.find({cuisine:"Bakery"},{name: "/^M/"}).toArray().length;
3. db.restaurants.find({cuisine:{$regex:".*Ice*."}}, {"address.zipcode":1})
4. db.restaurants.find({cuisine:"Chinese"},{"address.building":1,"address.street":1}, {$sort:{"address.zipcode":1}})
5. db.restaurants.find({borough:"Manhattan",cuisine:"American "})
6. db.restaurants.find({grades:{$size:4}})
7. db.restaurants.find({borough:"Manhattan"}, {name:1, grades:1,street:"Broadway"})
8. db.restaurants.find({borough:"Bronx"}).sort({"grades.score":1}).limit(5)
9. db.restaurants.find({borough:"Brooklyn"}).sort({name:1}).skip(20).limit(9)
10. db.restaurants.find({$or:[{cuisine:"Pizza"}, {cuisine:"Italian"}]}).sort({name:-1})
