#' Import necessary packages

library(worldfootballR)
library(ggshakeR)

#' Extracting the data. Use the function below, from worldfootballR to scrape the data.
#' Drop the link from the player's FBref page and change between the "primary" and "secondary" options 
#' for pos_versus to change the demographic of players the selected player is compared to.
#' 
#' Single player data exctraction and prep

data <- fb_player_scouting_report("https://fbref.com/en/players/7ba6d84e/David-de-Gea", pos_versus = "primary")

#' Plotting single player chart. The options for the template are :
#' forward, midfielder, winger, defender, full back and goalkeeper.
#' Use the correct season for the season parameter. It is recommended to copy and paste the names from the scouting_period column.  

plot <- plot_pizza(data = data, type = "single", template = "goalkeeper", 
                   colour_poss = "#41ab5d", colour_att = "#2171b5", season = "Last 365 Days", 
                   colour_def = "#fec44f", theme = "dark")
plot

#' Comparison chart data prep

data1 <- fb_player_scouting_report("https://fbref.com/en/players/5dcf3e90/Unai-Simon", pos_versus = "primary")
data2 <- fb_player_scouting_report("https://fbref.com/en/players/7ba6d84e/David-de-Gea", pos_versus = "primary")

data <- rbind(data1, data2)

#' Plotting comparison chart. Use player names without accents, 
#' for ex. write Dušan Vlahović as Dusan Vlahovic. 
#' In case of one player having less rows than required, 149 for outfield players,
#' 37 for goalkeepers, input that specific player as player_1 in the plot code.

plot <- plot_pizza(data = data, type = "comparison", template = "goalkeeper",
                   player_1 = "Unai Simon", player_2 = "David de Gea",
                   season_player_1 = "Last 365 Days", season_player_2 = "Last 365 Days",
                   colour_compare = "lightgreen", theme = "black")
plot

#' Saving the plot. Set working directory to the file where you 
#' want your plot exported. Change the slashes from (\) to (/).
#' Example:
#' Convert setwd("C:\Users\harsh_1mwi2o4\Downloads") to setwd("C:/Users/harsh_1mwi2o4/Downloads"), then run

setwd("C:/Users/harsh_1mwi2o4/Downloads")

#' Run these following lines depending on your operating system

## Windows

ggsave("image.png", bg = "black", width = 2500, height = 2800, units = "px")

## Mac

system("convert -trim image.png new_image.png")
