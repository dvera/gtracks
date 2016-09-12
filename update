#!/usr/bin/env bash

HUBDBID="1_IzQ4J_yi6m1WCO2PBo9_mqvse2ShGX2dEYaB1ncQcg"

E_OPTERROR=85

if [ $# -lt 1 ]    # Script invoked with no command-line args?
then
  echo "Usage: `basename $0` hubName"
  exit $E_OPTERROR    # Exit and explain usage.
    # Usage: scriptname -options
    # Note: dash (-) necessary
fi

#set -e

DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"

hubname=$1

>&2 echo "downloading hub list"

curl -sL "https://spreadsheets.google.com/feeds/download/spreadsheets/Export?key="$HUBDBID"&hl=en&exportFormat=tsv" | tr -d "\r" > $DIR/hubDb.tsv && echo "" >> $DIR/hubDb.tsv

ocols=$(head -n 1 hubDb.tsv)
tail -n+2 hubDb.tsv | while IFS=$'\t' read -r $ocols
do
  if [[ "$name" == "$hubname" ]] || [[ "$hubname" == "all" ]]; then

    mkdir -p $DIR/$name

    >&2 echo "downloading info for hub \"$name\""

    curl -sL "https://spreadsheets.google.com/feeds/download/spreadsheets/Export?key="$hubId"&hl=en&exportFormat=tsv" | tr -d "\r" > $DIR/$name/hub.tsv && echo "" >> $DIR/$name/hub.tsv

    grep -v '_genomes' $DIR/$name/hub.tsv | tr '\t' ' ' > $DIR/$name/hub.txt

    genomesId=$(grep _genomes $DIR/$name/hub.tsv | cut -f 2)

    curl -sL "https://spreadsheets.google.com/feeds/download/spreadsheets/Export?key="$_genomesId"&hl=en&exportFormat=tsv" | tr -d "\r" > $DIR/$name/genomes.tsv && echo "" >> $DIR/$name/genomes.tsv


    rm -f $DIR/$name/genomes.txt

    ### HTML ###
    gcols=$(head -n 1 $DIR/$name/genomes.tsv)
    tail -n+2 $DIR/$name/genomes.tsv | while IFS=$'\t' read -r $gcols
    do


      awk -F "\t" '{if(NR==1){split($0,xx,"\t"); nf=NF} ; if(NR>1 && $1==1){for (i = 1; i <= nf; i++) print xx[i]" "$i; print ""  }}' $DIR/$name/genomes.tsv | grep -v " NA$" | grep -v "^_" > $DIR/$name/genomes.txt


      mkdir -p $DIR/$name/$genome/bbi

      >&2 echo "downloading track table for \"$genome\""

      curl -sL "https://spreadsheets.google.com/feeds/download/spreadsheets/Export?key="$_genomeId"&hl=en&exportFormat=tsv" | tr -d "\r" > $DIR/$name/$genome/hubDb.tsv && echo "" >> $DIR/$name/$genome/hubDb.tsv

      >&2 echo "  creating track database file"

      awk -F "\t" '{if(NR==1){split($0,xx,"\t"); nf=NF} ; if(NR>1 && $1==1){for (i = 1; i <= nf; i++) print xx[i]" "$i; print ""  }}' $DIR/$name/$genome/hubDb.tsv | grep -v " NA$" | grep -v "^_" > $DIR/$name/$genome/hubDb.txt

    done # end genome loop

    # >&2 echo "updating hub on server"
    # >&2 echo "enter password for $userhost"
    #

    #scp -r $DIR/$hubname/ ${userhost}:$(dirname $path)

  fi # end hub

done
