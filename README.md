# flu structure probing data 
## Introduction
This repository contains bigWig files of influenza A virus (IAV) structure probing data publised in [N Takizawa and RK Kawaguchi, Comput Struct Biotechnol J. (2023)](https://www.sciencedirect.com/science/article/pii/S2001037023003926).
You can view these structure probing data of IAV using genome browser.
Here, I will also show how to view these data locally using [JBrowseR](https://gmod.github.io/JBrowseR/index.html).

## probing data
bigWig files of IAV structure probing data are in dataset folder. There are 12 bigWig files and reference sequence files in the folder.  
reactIDR_virion_SHAPE.bw  
reactIDR_vRNP_SHAPE.bw  
reactIDR_vRNA_SHAPE.bw  
BUMHMM_virion_SHAPE.bw  
BUMHMM_vRNP_SHAPE.bw  
BUMHMM_vRNA_SHAPE.bw  
reactIDR_virion_DMS.bw  
reactIDR_vRNP_DMS.bw  
reactIDR_vRNA_DMS.bw  
BUMHMM_virion_DMS.bw  
BUMHMM_vRNP_DMS.bw  
BUMHMM_vRNA_DMS.bw  
PR8_local_vRNA.fa.gz  
PR8_local_vRNA.fa.gz.fai  
PR8_local_vRNA.fa.gz.gzi

## Browse using JBrowseR
### Before start
R and Rstudio must be installed.
Download dataset folder from code -> Download ZIP.

### Install JBrowseR and shiny
You can install JBrowseR and shiny on RStudio from CRAN with:
```
install.packages("JBrowseR")
install.packages("shiny")
```
If already installed, launch shiny and JBrowseR
```
library(JBrowseR)
library(shiny)
```

### Data folder
Loads a data folder. Put the path of the downloaded data folder in (your data folder path).
```
data_server <- serve_data("(your data folder path)")
```
The data server starts up. If you need to close the data server, you can do so with the following command.
```
data_server$stop_server()
```

### Run JBrowseR and view probing data
Paste and execute the following command in Rstudio.
```
ui <- fluidPage(
  titlePanel("Flu structure data"),
  # this adds to the browser to the UI, and specifies the output ID in the server
  JBrowseROutput("browserOutput")
)

server <- function(input, output, session) {
  # create the necessary JB2 assembly configuration
  assembly <- assembly(
    "http://127.0.0.1:5000/PR8_local_vRNA.fa.gz",
    bgzip = TRUE
  )

 # create configuration for a JB2 bigWig Track
  rI_virion_SHAPE_track <- track_wiggle(
    "http://127.0.0.1:5000/reactIDR_virion_SHAPE.bw",
    assembly
  )

  rI_vRNP_SHAPE_track <- track_wiggle(
    "http://127.0.0.1:5000/reactIDR_vRNP_SHAPE.bw",
    assembly
  )

  rI_vRNA_SHAPE_track <- track_wiggle(
    "http://127.0.0.1:5000/reactIDR_vRNA_SHAPE.bw",
    assembly
  )

  BH_virion_SHAPE_track <- track_wiggle(
    "http://127.0.0.1:5000/BUMHMM_virion_SHAPE.bw",
    assembly
  )

  BH_vRNP_SHAPE_track <- track_wiggle(
    "http://127.0.0.1:5000/BUMHMM_vRNP_SHAPE.bw",
    assembly
  )

  BH_vRNA_SHAPE_track <- track_wiggle(
    "http://127.0.0.1:5000/BUMHMM_vRNA_SHAPE.bw",
    assembly
  )

  rI_virion_DMS_track <- track_wiggle(
    "http://127.0.0.1:5000/reactIDR_virion_DMS.bw",
    assembly
  )

  rI_vRNP_DMS_track <- track_wiggle(
    "http://127.0.0.1:5000/reactIDR_vRNP_DMS.bw",
    assembly
  )

  rI_vRNA_DMS_track <- track_wiggle(
    "http://127.0.0.1:5000/reactIDR_vRNA_DMS.bw",
    assembly
  )

  BH_virion_DMS_track <- track_wiggle(
    "http://127.0.0.1:5000/BUMHMM_virion_DMS.bw",
    assembly
  )

  BH_vRNP_DMS_track <- track_wiggle(
    "http://127.0.0.1:5000/BUMHMM_vRNP_DMS.bw",
    assembly
  )

  BH_vRNA_DMS_track <- track_wiggle(
    "http://127.0.0.1:5000/BUMHMM_vRNA_DMS.bw",
    assembly
  )

  # create the tracks array to pass to browser
  tracks <- tracks(rI_virion_SHAPE_track, rI_vRNP_SHAPE_track, rI_vRNA_SHAPE_track, BH_virion_SHAPE_track, BH_vRNP_SHAPE_track, BH_vRNA_SHAPE_track, rI_virion_DMS_track, rI_vRNP_DMS_track, rI_vRNA_DMS_track, BH_virion_DMS_track, BH_vRNP_DMS_track, BH_vRNA_DMS_track)

  # link the UI with the browser widget
  output$browserOutput <- renderJBrowseR(
    JBrowseR(
      "View",
      assembly = assembly,
	  tracks = tracks
    )
  )
}

shinyApp(ui, server)
```
The Shiny window will be launched. The page is blank in my windows environment, but I was able to use it by pressing the "Open in Browser" button at the top and launching the browser. Click on "open" first, then "OPEN TRACK SELECTOR" on the next screen. Check the data to be displayed and click outside the window to display the data. Enjoy!

## Future plan
integrate flu structure probing data reported by other labs  
integrate NP CLIP data  
Web server...

## Reference
Comprehensive in virio structure probing analysis of the influenza A virus identifies functional RNA structures involved in viral genome replication.  
N. Takizawa and R.K. Kawaguchi  
Computational and Structural Biotechnology Journal, 21, 5259-5272 (2023)  
DOI: [https://doi.org/10.1016/j.csbj.2023.10.036](https://doi.org/10.1016/j.csbj.2023.10.036)
