# gtracks
A simple script for creating and maintaining UCSC genome browser track/assembly hubs using google spreadsheets

## why

The [UCSC Genome Browser](http://genome.ucsc.edu) is a web-based genome browser widely used for viewing and sharing various types of genomic data mapped to reference genomes. [Track hubs](https://genome.ucsc.edu/goldenPath/help/hgTrackHubHelp.html) allow users to create and maintain a stable database of custom tracks for viewing in the browser. Additionally, an [assembly hub](https://genome.ucsc.edu/goldenPath/help/hubQuickStartAssembly.html) is a type of track hub that allows users to explore other reference genomes not hosted at UCSC. Creating and maintaining multiple hubs with a large number of tracks is difficult and time-consuming because the markup-type language used to define hubs, while allowing for complex track relationships to be defined, becomes difficult to maintain with a large number of tracks.

## how

Track/assembly hubs are entirely defined by a set of files stored by the user on a web server that the UCSC browser can access via http. gtracks is a bash script that allows users to define and maintain multiple track/assembly hubs in a set of google spreadhsheets, which are much easier to maintain by humans for a large number of tracks and hubs. From your web server hosting the data, gtracks downloads these google spreadsheets and processes them into the set of files required to define a track/assembly hub, including creating the entire directory structure for each hub if it isn't already present. Apart from the google spreadsheets, the only other information that needs to be maintained by the user are the files corresponding to the data tracks to be loaded. Below shows an example set of track/assembly hubs. The only files that need to be maintained by the user, which are starred below, are the data files for each track, and in the case of assembly hubs, the 2bit file containing the reference genome sequence.

    hubs/ - directory containing a set of track/assembly hubs to be managed by gtracks
        gtracks.sh - the gtracks shell script
        trackHub1/ - directory containing files for trackHub1
             hub.txt -  a short description of hub properties
             genomes.txt - list of genome assemblies included in the hub data
             hg19/ - directory for the hg19 human assembly
                  trackDb.txt - display properties for tracks in this directory
                  bbi/ - directory of data files containing the data to be displayed for hg19
                      *dnaseLiver.bigWig - wiggle plot of DNase in liver
                      *dnaseLiver.bigBed - regions of active DNase
             hg18/ - directory of data for the hg18 human assembly
                  trackDb.txt - display properties for tracks in this directory
                  bbi/ - directory of data files containing the data to be displayed for hg18
                      *dnaseLiver.bigWig - wiggle plot of DNase data in liver
                      *dnaseLiver.bigBed - regions of active DNase
        assemblyHub1/ - directory containing files for assemblyHub1
             hub.txt -  a short description of hub properties
             genomes.txt - list of genome assemblies included in the hub data
             newOrg1/ - directory for the newOrg1 assembly
                  trackDb.txt – definitions for tracks on this genome assembly
                  *genome.2bit – ‘2bit’ file constructed from your fasta sequence
                  bbi/ - directory of data files containing the data to be displayed for hg19
                      *dnaseLiver.bigWig - wiggle plot of DNase in liver
                      *dnaseLiver.bigBed - regions of active DNase
             newOrg2/ - directory for the newOrg2 assembly
                  trackDb.txt – definitions for tracks on this genome assembly
                  *genome.2bit – ‘2bit’ file constructed from your fasta sequence
                  bbi/ - directory of data files containing the data to be displayed for hg19
                      *dnaseLiver.bigWig - wiggle plot of DNase in liver
                      *dnaseLiver.bigBed - regions of active DNase

If a user does not have access to such a server, one can easily and cheaply generate one on a cloud service provider such as Digital Ocean.

## to do
- automate generation and sharing of google spreadsheets
- error handling
- more docs
- allow an entire hub to be defined in multiple sheets within the same google spreadsheet
- create cloudinit to help users quickly spin up a web server to host hubs
