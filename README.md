
**COMPANY** : CODTECH IT SOLUTIONS

 **NAME** : NERUSU MADHU JAHNAVI

**INTERNID** : CT6WNSZ

**DOMAIN** : POWER BI

**DURATION** : 6 WEEKS

 DESCRIPTION 
    
  ****Integration with R****


### Steps to Use R Scripts in Power BI:
1. **Install R**: 
   Before using R in Power BI,  need to install R on  system.

2.  **Enable R in Power BI**:
   - Open Power BI Desktop.
   - Go to File- Options and Settings-Options
   - In the Options window, navigate to the R scripting section under the Global settings.
   - Specify the R home directory where R is installed.

*** Using R Scripts for Data Analysis and Visualization
R Visual for Advanced Visualization
1. **Create an R Visual**:
   - In the Power BI report view, click on the R icon in the Visualizations pane.
   - In the R script editor, write  R code to generate a custom plot. For instance, want to plot a regression line for sales data.
     
### Example 1:   ** R  code for a scatter plot with a regression line**

   Load necessary libraries
   
   library(ggplot2)

   # Create a scatter plot with a regression line
   ggplot(dataset, aes(x = Age, y = Sales)) +
     geom_point() + 
     geom_smooth(method = "lm", col = "red") +
     theme_minimal() +
     ggtitle("Sales vs Age with Regression Line")

2. **Bind the Fields**:
   - Drag the relevant fields (Age,Sales ) into the R visuals data field well.
   - The R visual will generate the plot based on your R script.
   
3. **Customize the Plot**:
   - It further customize the plot using standard 'ggplot2' options or use other R libraries depending on needs.
  
    ##Save the report and Publish##
     
Output Report :

![Integration with R -example1- output](https://github.com/user-attachments/assets/14613fe6-ca4f-40a8-b456-bcba4b9c427a)



   
### Example 2 : Create a Heatmap in Power BI Using R
 
1. **Add R Visual for Heatmap**:
   - Select the R visual from the visualization pane.
   - Take another dataset contains (Weekdays,Time of days...)
   - In the R script editor, write the following R code:
  
     
     library(dplyr) #count
library(ggplot2) # Visualization
library(ggthemes) # tufte theme
library(zoo) #rollapply

# Convert timestamp to POSIXct.
dataset$Timestamp <-as.POSIXct(dataset$Timestamp,format="%Y-%m-%dT%H:%M:%OS")

#Create a dataframe containing the weekday and hour of a call, and summarise per day/hour
calls <- data.frame(weekday=weekdays(dataset$Timestamp), hour = format(dataset$Timestamp,"%H"))
sumCalls <- count(calls, weekday, hour)

#Create an array of weekdays and use it to correctly order the weekdays (mon-sun)
days.of.week <- weekdays(x=as.Date(seq(7), origin="1950-01-01"))
sumCalls$weekday <- factor(sumCalls$weekday, rev(days.of.week))

# Convert the continous scale to a descrete scale based on the unique n's. Define the color range and create an appropriate label. 
quantile.range <- quantile(unique(sumCalls$n), probs = seq(0, 1, 0.2))
color.palette <- colorRampPalette(c("#00FF00", "#0000FF"))(length(quantile.range) - 1)
label.text <- rollapply(round(quantile.range, 2), width = 2, by = 1, FUN = function(i) paste(i, collapse = " - "))
sumCalls$discrete <- findInterval(sumCalls$n, quantile.range, all.inside = TRUE)
 
# Visualization.
ggplot(sumCalls, aes(x=hour, y=weekday, fill=factor(discrete))) +
  geom_tile(color="red", size=0.1) +
  coord_equal() +
  labs(x=NULL, y=NULL, title="Calls per weekday & time of day") +
  scale_fill_manual(values = color.palette, name = "", labels = label.text) +
  theme_tufte()

   This code will create a heatmap where the intensity of the color indicates the Calls heatmap per weekday and timestamp
   
   ##Save the report and Publish##

 Output Report:

   ![Integration with R -example 2 -output](https://github.com/user-attachments/assets/203a2f9e-3495-4f37-bae4-f68ef8b9629a)


    






