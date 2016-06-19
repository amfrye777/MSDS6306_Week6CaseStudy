Assignment Definition
---------------------

-   Deliverable: Markdown file uploaded to GitHub containing the
    following
-   Introduction to the project. The introduction should not start with
    “For my project I …”. The introduction needs to be written as if you
    are presenting the work to someone who has given you the data to
    analyze and wants to understand the result. In other words, pretend
    it’s not a case study for a course. Pretend it’s a presentation for
    a client.
-   Code for downloading, tidying, and merging data in a R
    Markdown file.
-   Brief explanations of the purpose of the code. The explanations
    should appear as a sentence or two before or after the code chunk.
    Even though you will not be hiding the code chunks (so that I can
    see the code), you need to pretend like the client can’t see them.
-   Code to answer the five questions above (plus the answers) in the
    same R Markdown file.
-   Clear answers to the questions, including interpretation of
    the plots.
-   Conclusion to the project. Summarize your findings from
    this exercise.
-   The file must be readable in GitHub – 5 points off if I have to
    download the file to read it! In other words, don’t forget to keep
    the md file!!

FILE TREE STRUCTURE DEFINED
---------------------------

    ## -- DataAnalysis
    ##    |__Question1.RMD
    ##    |__Question2.RMD
    ##    |__Question3.RMD
    ##    |__Question4.RMD
    ##    |__Question5.RMD
    ## -- DataCleanup
    ##    |__CleanEducation.RMD
    ##    |__CleanProduct.RMD
    ## -- DataLoad
    ##    |__Education.csv
    ##    |__LoadEducation.RMD
    ##    |__LoadProduct.RMD
    ##    |__Products.csv
    ## -- MSDS6306_Week6CaseStudy.Rproj
    ## -- Paper
    ##    |__Afrye_Week6CaseStudy.md
    ##    |__Afrye_Week6CaseStudy.RMD
    ##    |__Afrye_Week6CaseStudy_files
    ##       |__figure-markdown_strict
    ##          |__Q4_DensityPlotLogTransformed-1.png
    ##          |__Q4_DensityPlotRaw-1.png
    ## -- README.md
    ## -- README.rmd
    ## -- RResources
    ##    |__Twee.R

**NOTE:** Project Deliverable File Located:
"~/Paper/AFrye\_Week6CaseStudy.MD"

PROJECT REPRODUCIBILITY INSTRUCTIONS
------------------------------------

1.  Regenerate README (If Project File Structure Changes)
    -   Open README.RMD located inside Project Root
    -   Modify DefaultDir input to your Project's Root Directory Path
    -   Knit README.Rmd

2.  Regenerate AFrye\_Week6CaseStudy.MD
    -   Open AFrye\_Week6CaseStudy.RMD
    -   Modify DefaultDir input to your Project's Root Directory Path
    -   Ensure all required R Packages are installed on your machine.
        Uncomment any needed Install.Packages code lines
    -   Knit AFrye\_Week6CaseStudy.RMD
