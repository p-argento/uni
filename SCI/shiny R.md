

```r
ui <- fluidPage(
  titlePanel("What's in a Name?"),
  # Add select input named "sex" to choose between "M" and "F"
  selectInput('sex', 'Select Sex', choices = c("F", "M")),
  # Add slider input named "year" to select year between 1900 and 2010
  sliderInput('year', 'Select Year', min = 1900, max = 2010, value = 1900),
  # CODE BELOW: Add table output named "table_top_10_names"
  tableOutput('table_top_10_names')
)

server <- function(input, output, session){
  # Function to create a data frame of top 10 names by sex and year 
  top_10_names <- function(){
    babynames %>% 
      filter(sex == input$sex) %>% 
      filter(year == input$year) %>% 
      slice_max(prop, n = 10)
  }
  # CODE BELOW: Render a table output named "table_top_10_names"
  output$table_top_10_names <- renderTable({top_10_names()})

}

shinyApp(ui = ui, server = server)
```

Building Shiny apps: 4 steps 
1. Add inputs (UI) 
2. Add outputs (UI/Server) 
3. Update layout (UI) 
4. Update outputs (Server)

```r
ui <- fluidPage(
  titlePanel('Most Popular Names'),
  sidebarLayout(
      sidebarPanel(
          selectInput('sex', 'Select Sex', selected='F', choices=c('M','F')),
          sliderInput('year', 'Select Year', value=1880, min=1880, max=2017)
      ),
      mainPanel(
          plotOutput('plot')
      )    
  )
)

server <- function(input, output, session) {
    output$plot <- renderPlot({
        ggplot(get_top_names(input$year, input$sex),aes(x=name,y=prop))+
            geom_col()
    })
}

shinyApp(ui = ui, server = server)
```