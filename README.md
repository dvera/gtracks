# gtracks
A simple script for creating and maintaining UCSC genome browser track/assembly hubs using google spreadsheets

## why

The [UCSC Genome Browser](http://genome.ucsc.edu) is a web-based genome browser widely used for viewing and sharing various types of genomic data mapped to reference genomes. [Track hubs](https://genome.ucsc.edu/goldenPath/help/hgTrackHubHelp.html) allow users to create and maintain a stable database of custom tracks for viewing in the browser. Additionally, an [assembly hub](https://genome.ucsc.edu/goldenPath/help/hubQuickStartAssembly.html) is a type of track hub that allows users to explore other reference genomes not hosted at UCSC. Creating and maintaining multiple hubs with a large number of tracks is difficult and time-consuming because the markup-type language used to define hubs. while the markup language allows complex track relationships to be defined, it becomes difficult to maintain with a large number of tracks.

## how

gtracks is a bash script that allows users to define and maintain multiple track/assembly hubs in a set of google spreadhsheets, which are much easier to maintain by humans for a large number of tracks and hubs. On your web server hosting the data, gtracks downloads these google spreadsheets and processes them into the set of files required to define a track/assembly hub.

The data for a track/assembly hub is stored by the user in a web-accessible server that can serve files via http using, for example, apache or nginx. If a user does not have access to such a server, one can easily and cheaply generate one on a cloud service provider such as Digital Ocean.


    myHub/ - directory containing track hub files
         hub.txt -  a short description of hub properties
         genomes.txt - list of genome assemblies included in the hub data
         hg19/ - directory for the hg19 (GRCh37) human assembly
              trackDb.txt - display properties for tracks in this directory
              bbi/ - directory of data files containing the data to be displayed for hg19
                  dnase.html - description text for a DNase track 
                  dnaseLiver.bigWig - wiggle plot of DNase in liver
                  dnaseLiver.bigBed - regions of active DNase
         hg18/ - directory of data for the hg18 (Build 36) human assembly
              trackDb.txt - display properties for tracks in this directory
              bbi/ - directory of data files containing the data to be displayed for hg18
                  dnase.html - description text for a DNase track 
                  dnaseLiver.bigWig - wiggle plot of DNase data in liver
                  dnaseLiver.bigBed - regions of active DNase
                  dnaseLung.bigWig - wiggle plot of DNase data in lung
                  dnaseLung.bigWig - regions of active DNase

## to do
- automate generation and sharing of google spreadsheets
- error handling
- more docs
- allow an entire hub to be defined in multiple sheets within the same google spreadsheet
