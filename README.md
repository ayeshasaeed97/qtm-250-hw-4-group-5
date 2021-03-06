Within this repo contains our Jupyter notebook of our research. The question we researched was how accurately could the Natural Language API detect the tone of language used in Amazon product reviews. We found this question to be important because reviews can greatly sway consumer opinion. We wanted to see how the API can measure wording on reviews for products that are overall rated above 4 stars. The reviews themselves range from good (3-5) to bad (1-2), so we choose one good and one bad per product to test the API's ability to accurately distinguish language.

To use the API, you must create an API key and input that into the get.pass function, and then ensure it has been saved. 

For the actual code to use the API, here it is below: 

wlservice = build('language', 'v1beta1', developerKey=APIKEY)

quotes = [
      'Include review here, with sentences separated by quotations marks and commas.']
for quote in quotes:
  response = lservice.documents().analyzeSentiment(
    body={
      'document': {
         'type': 'PLAIN_TEXT',
         'content': quote
      }
    }).execute()
  
  polarity = response['documentSentiment']['polarity']
  
  magnitude = response['documentSentiment']['magnitude']
  
  print('POLARITY=%s MAGNITUDE=%s for %s' % (polarity, magnitude, quote))
  
  
From this code, you will reveive an output of the polarity and magnitude per sentence in the included quotations. The polarity essentially determines if the uploaded phrase is positive or negative while the magnitude tells you the severity or the extent of that phrase. For example, dislike has a lower magnitude than hate, but both have a polarity of (-1).

