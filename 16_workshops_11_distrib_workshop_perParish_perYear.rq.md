#+ summary: How many workshops are there per parish over the years? 
#+ endpoint: http://128.178.60.47:8890/sparql
#+ method: GET
#+ tags:
#+  - 16_workshop

```sparql
SELECT ?year ?labelParish (COUNT (distinct ?workshop) AS ?NbWorkshop)
WHERE
{
  ?workshop a grz-owl:WorkshopMention .
  ?workshop grz-owl:hasLocation/common:inParish ?parish .
  ?parish rdfs:label ?labelParish . 
  ?workshop grz-owl:isWorkshopOf/core:isMentionedIn/sem:hasTimeStamp ?date
  BIND(year(?date) AS ?year)

}
GROUP BY ?labelParish  ?year
ORDER BY ASC (?year)
```
