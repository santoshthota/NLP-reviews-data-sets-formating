# Product-reviews-analysis-useful-scripts-for-NLP-problem
This will have script to modify regular datasets of reviews used in NLP problem to neat json format for easy use.

The input file Nokia6610.txt is
*****************************************************************************
* Annotated by: Minqing Hu and Bing Liu, 2004.
*		Department of Computer Sicence
*               University of Illinois at Chicago              
*
* Product name: Nokia 6610
* Review Source: amazon.com
*
* See Readme.txt to find the meaning of each symbol. 
*****************************************************************************

Eg output format:
{"reviews":[
  {"id":1,"title":"excellent phone , excellent service .",
    "sentences":[
      {"id":"1_1","text":"i am a business user who heavily depend on mobile service .","features":[]},
      {"id":"1_2","text":"there is much which has been said in other reviews about the features of this phone",
      "features":[
        {"id":"1_2_1","name":"phone","opinion":"+3","u":false,"p":false},
        {"id":"1_2_2","name":" work","opinion":"+2","u":false,"p":false}]}
      ]
  }
]}
