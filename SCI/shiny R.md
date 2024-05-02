

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

## Reactivity
```r
ui <- fluidPage(
  titlePanel('BMI Calculator'),
  sidebarLayout(
    sidebarPanel(
      numericInput('height', 'Enter your height in meters', 1.5, 1, 2),
      numericInput('weight', 'Enter your weight in Kilograms', 60, 45, 120)
    ),
    mainPanel(
      textOutput("bmi"),
      textOutput("bmi_range")
    )
  )
)

server <- function(input, output, session) {
  # CODE BELOW: Add a reactive expression rval_bmi to calculate BMI
  rval_bmi <- reactive({input$weight/(input$height^2)})
  
  
  output$bmi <- renderText({
    # MODIFY CODE BELOW: Replace right-hand-side with reactive expression
    bmi <- rval_bmi()
    paste("Your BMI is", round(bmi, 1))
  })
  output$bmi_range <- renderText({
    # MODIFY CODE BELOW: Replace right-hand-side with reactive expression
    bmi <- rval_bmi()
    bmi_status <- cut(bmi, 
      breaks = c(0, 18.5, 24.9, 29.9, 40),
      labels = c('underweight', 'healthy', 'overweight', 'obese')
    )
    paste("You are", bmi_status)
  })
}

shinyApp(ui = ui, server = server)
```

Add an observer to display notifications.
Recall that an observer is used for side effects, like displaying a plot, table, or text in the browser. By default an observer triggers an action, whenever one of its underlying dependencies change.
As we are triggering an action using an observer, we do NOT need to use a `render***()` function or assign the results to an `output`.

### eventReactive()
The function `eventReactive()` is used to compute a reactive value that only updates in response to a specific event.
```r
ui <- fluidPage(
  titlePanel('BMI Calculator'),
  sidebarLayout(
    sidebarPanel(
      textInput('name', 'Enter your name'),
      numericInput('height', 'Enter height (in m)', 1.5, 1, 2, step = 0.1),
      numericInput('weight', 'Enter weight (in Kg)', 60, 45, 120),
      actionButton("show_bmi", "Show BMI")
    ),
    mainPanel(
      textOutput("bmi")
    )
  )
)

server <- function(input, output, session) {
  # MODIFY CODE BELOW: Use eventReactive to delay the execution of the
  # calculation until the user clicks on the show_bmi button (Show BMI)
  rval_bmi <- eventReactive(input$show_bmi,{
    input$weight/(input$height^2)
  })
  output$bmi <- renderText({
    bmi <- rval_bmi()
    paste("Hi", input$name, ". Your BMI is", rval_bmi)
  })
}

shinyApp(ui = ui, server = server)
```

### observeEvent()
There are times when you want to perform an action in response to an event.
The `observeEvent()` function allows you to achieve this. It accepts two arguments:
1. The event you want to respond to.
2. The function that should be called whenever the event occurs.
```r
ui <- fluidPage(
  titlePanel('BMI Calculator'),
  sidebarLayout(
    sidebarPanel(
      textInput('name', 'Enter your name'),
      numericInput('height', 'Enter your height in meters', 1.5, 1, 2),
      numericInput('weight', 'Enter your weight in Kilograms', 60, 45, 120),
      actionButton("show_bmi", "Show BMI"),
      # CODE BELOW: Add an action button named "show_help"
      actionButton("show_help", "Help")
    ),
    mainPanel(
      textOutput("bmi")
    )
  )
)

server <- function(input, output, session) {
  # MODIFY CODE BELOW: Wrap in observeEvent() so the help text 
  # is displayed when a user clicks on the Help button.
  
     # Display a modal dialog with bmi_help_text
     # MODIFY CODE BELOW: Uncomment code
  observeEvent(input$show_help, {
    showModal(modalDialog(bmi_help_text))
  })
  
  rv_bmi <- eventReactive(input$show_bmi, {
    input$weight/(input$height^2)
  })
  output$bmi <- renderText({
    bmi <- rv_bmi()
    paste("Hi", input$name, ". Your BMI is", round(bmi, 1))
  })
}

shinyApp(ui = ui, server = server)
```

### from shiny docs
https://shiny.posit.co/r/articles/build/reactivity-overview/

In Shiny, there are three kinds of objects in reactive programming: reactive sources, reactive conductors, and reactive endpoints, which are represented with these symbols:

![[Pasted image 20240430143805.png]]

In a Shiny application, the source typically is user input through a browser interface. For example, when the user selects an item, types input, or clicks on a button, these actions will set values that are reactive sources. A reactive endpoint is usually something that appears in the user’s browser window, such as a plot or a table of values.

![[Pasted image 20240430143907.png]]

It’s also possible to put reactive components in between the sources and endpoints. These components are called _reactive conductors_.
it can be both a parent and child in a graph of the reactive structure. Sources can only be parents (they can have dependents), and endpoints can only be children (they can be dependents) in the reactive graph.

Keep in mind that if your application tries to access reactive values or expressions from outside a reactive context — that is, outside of a reactive expression or observer — then it will result in an error. You can think of there being a reactive “world” which can see and change the non-reactive world, but the non-reactive world can’t do the same to the reactive world.


- **Reactive sources** can signal objects downstream that they need to re-execute.
- **Reactive conductors** are placed somewhere in between sources and endpoints on the reactive graph. They are typically used for encapsulating slow operations.
- **Reactive endpoints** can be told to re-execute by the reactive environment, and can request _upstream_ objects to execute.
- **Invalidation arrows** diagram the flow of invalidation events. It can also be said that the child node is a **dependent of** or **takes a dependency on** the parent node.

Presently, Shiny has one class of objects that act as reactive sources, one class of objects that act as reactive conductors, and one class of objects that act as reactive endpoints, but in principle there could be other classes that implement these roles.

- **Reactive values** are an implementation of Reactive sources; that is, they are an implementation of that role.
- **Reactive expressions** are an implementation of Reactive conductors. They can access reactive values or other reactive expressions, and they return a value.
- **Observers** are an implementation of Reactive endpoints. They can access reactive sources and reactive expressions, and they don’t return a value; they are used for their side effects.

![[Pasted image 20240430144750.png]]


## Shiny app
```r
ui <- fluidPage(
  titlePanel("UFO Sightings"),
  sidebarLayout(
    sidebarPanel(
      selectInput("state", "Choose a U.S. state:", choices = unique(usa_ufo_sightings$state)),
      dateRangeInput("dates", "Choose a date range:",
                     start = "1920-01-01",
                     end = "1950-01-01")
    ),
    mainPanel(
      tabsetPanel(
        tabPanel(
          # Add plot output named 'shapes'
          "Plot",
          plotOutput("shapes")
        ),
        tabPanel(
          # Add table output named 'duration_table'
          "Table",
          tableOutput("duration_table")
        )
      )
    )
  )
)

server <- function(input, output) {
  # CODE BELOW: Create a plot output of sightings by shape,
  # For the selected inputs
  output$shapes <- renderPlot({
    usa_ufo_sightings %>%
      filter(state == input$state) %>%
      filter(date_sighted >= input$dates[1] & date_sighted <= input$dates[2]) %>%
      ggplot(aes(shape))+
        geom_bar()
  })
  
  
  # CODE BELOW: Create a table output named 'duration_table', by shape,
  # of # sighted, plus mean, median, max, and min duration of sightings
  # for the selected inputs
  output$duration_table <- renderTable({
    usa_ufo_sightings %>%
      filter(state == input$state) %>%
      filter(date_sighted >= input$dates[1] & date_sighted <= input$dates[2]) %>%
      group_by(shape) %>%
      summarise(avg=mean(n()), median=median(n()), min=min(date_sighted),max=max(date_sighted))
  })
  
  
}

shinyApp(ui, server)
```

## ShinyWidgets
`shinyWidgetsGallery()`
Let's look at all the different input options that are already built for you by exploring the `shinyWidgets` package. It comes with a neat built-in function, `shinyWidgetsGallery()` that opens a pre-built Shiny app that allows you to explore these pre-built inputs **and** gives you the code for implementing them.






# IreneSpada Lecture

## Principles of DataViz

> The purpose of DataViz is insight, not pictures.

Two principles
1. Design for ensuring clarity, precision, efficiency
2. Maximize ideas, minimize ink.

Emphasize the message you want to convey. Using colors and arrows, for example.

Animation vs interaction.

In a interaction, keep in mind your user
1. provide instructions
2. limit overwhelming interactions
	1. similar to minimize ink (loose the why)


Check responsiveness!!

https://ispada.shinyapps.io/AppTopicUni/
Here the data 

