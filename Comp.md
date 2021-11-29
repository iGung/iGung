library(worldfootballR)
library(ggshakeR)

data <- fb_player_scouting_report("https://fbref.com/en/players/7ba6d84e/David-de-Gea", pos_versus = "primary")

plot <- plot_pizza(data = data, type = "single", template = "goalkeeper", 
                   colour_poss = "#41ab5d", colour_att = "#2171b5", season = "Last 365 Days", 
                   colour_def = "#fec44f", theme = "dark")
plot

data1 <- fb_player_scouting_report("https://fbref.com/en/players/5dcf3e90/Unai-Simon", pos_versus = "primary")
data2 <- fb_player_scouting_report("https://fbref.com/en/players/7ba6d84e/David-de-Gea", pos_versus = "primary")

data <- rbind(data1, data2)

plot <- plot_pizza(data = data, type = "comparison", template = "goalkeeper",
                   player_1 = "Unai Simon", player_2 = "David de Gea",
                   season_player_1 = "Last 365 Days", season_player_2 = "Last 365 Days",
                   colour_compare = "lightgreen", theme = "black")
plot

setwd("C:/Users/stvnj/Desktop/Screenshots/Comparisons")

ggsave("image.png", bg = "black", width = 2500, height = 2800, units = "px")
