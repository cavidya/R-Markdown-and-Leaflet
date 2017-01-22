#Interactive Data Mapping - Data Products - Coursera
Vidya Cuddalore Arivudainambi

#January 21, 2017

Interactive Map Assignment: Developing Data Products
Create a web page using R Markdown that features a map created with Leaflet.

Host your webpage on either GitHub Pages, RPubs, or NeoCities.

Your webpage must contain the date that you created the document, and it must contain a map created with Leaflet. We would love to see you show off your creativity!

Submission
By accessing the Open Data NYC api we can look at art museum locations in New York City.

library(jsonlite)
library(leaflet)
data <- fromJSON("https://data.cityofnewyork.us/resource/43hw-uvdj.json", flatten = TRUE)

artLatLong <- data.frame(
  lat = unlist(lapply(data$the_geom.coordinates, `[[`, 2)),
  lng = unlist(lapply(data$the_geom.coordinates, `[[`, 1))
)

artIcons <- makeIcon(
  iconUrl = "https://people.ucsc.edu/~admcnich/images/pin.svg",
  iconWidth = 35*215/230, iconHeight = 35,
  iconAnchorX = 35*215/230/2, iconAnchorY = 35
)

artSites <- paste("<a href='", data$url, "'>",data$name,"</a>" ,sep = "")

January 21, 2017

Map of Art Museums in NYC

artLatLong %>% leaflet() %>% addTiles() %>%
addMarkers(icon=artIcons, popup = artSites)
