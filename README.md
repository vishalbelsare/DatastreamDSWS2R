# DatastreamDSWS2R
Functions and a R5 class that allows data to be downloaded and uploaded to the Thomson Reuters Datastream database via the DSWS server.  Thomson Reuters Datastream is a rich database of financial information.  You need to have a Datastream subscription and a username/password to use this package.

The package can be installed using:

    require(devtools)
    install_github(“CharlesCara/DatastreamDSWS2R”)

Your Thomson Reuters Datastream username and password need to be saved in options().  We suggest you add these lines to your .RProfile file:

    options(Datastream.Username = "YOURUSERNAME")
    options(Datastream.Password = "YOURPASSWORD")

A typical request would be for a snapshot request:

     mydsws <- dsws$new()
     myData <- mydsws$snapshotRequest(instrument = c("ABF","RIO","WPP"),
                                   datatype = "P",
                                   requestDate = "0D")

or with expressions (including E codes), where "X" is replaced by "XXXX":

     mydsws <- dsws$new()
     myData <- mydsws$snapshotRequest(instrument = c("ABF","RIO","WPP"),
                                   expression = "PCH#(XXXX,3M)",
                                   requestDate = "0D")

and for a constituent list request (expressions are also supported)

    mydsws <- dsws$new()
    myData <- mydsws$listRequest(instrument = "LFTSE100", datatype = "P", requestDate = "0D")

and for a timeseries request (expressions are also supported)

    mydsws <- dsws$new()
    xtsData <- mydsws$timeSeriesRequest(instrument = "MKS",
                           datatype = "MV",
                           startDate = "-30D",
                           endDate = "-0D",
                           frequency = "D")


In addition, this package has been built to be largely backwards compatible with the [Datastream2R](https://github.com/CharlesCara/Datastream2R) package.  You just need to replace 
    require(Datastream2R) 
with 
    require(DatastreamDSWS2R)


