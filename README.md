# Auto-Suggest-and-Auto-complete-using-C-
PROJECT OVERVIEW :-

We all know that trie is tree like data structure which is used to store key . Main advantage of trie is  searching a key . This can be done be in O( length_of_key ) which is very fast in compare to naive search where we check for every word in our collections that it matches with key.

Now consider a scenario where a user is typing and in mid way all suggestion( words which user actually wants to type ) just pops up .
This feature can be implements with the help of trie. 


We can store all the words which are most used or which are most typed by user in past . Now whenever user types a prefix , our algorithm will find all suggestion ( or words ) which user actually want to type.     


All utility function (like searching ,addition , deletion , auto_complete ) are implemented in C++.


We can modify our "trienode structure" to store frequency of word . Every time a word is suggested( user used this suggestion ) or user typed it himself we increase this frequency variable . This frequency variable help us to suggest most frequent word to user. 
We can modify structure to hold all letter ( A-Z , a-z ). 
