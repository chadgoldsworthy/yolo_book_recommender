<h1>The YOLO book recommender</h1>
The idea for this project was to get personalised book recommendations by taking a picture of your book shelf, or any bookshelves that sparks your interest. The network recognises the books on your bookshelf, and suggests some additional books you may like.

<b>High level functionality:</b>

* model_init() initialises the YOLO model, v3 in this example.
* crop_books() passes the image through the model to detect the individual books and crop them.
* extract_books() extracts the text from each of the books using pytesseract and uses isbntools to collect the books meta data
* google_recommender() finds similar books through the Google Books API.
* print_recommendations() prints a specified num of recommendations to screen. 

<h2>Visual representation of the model:</h2>

After initialising the model, the ```crop_books()``` function detects the bounding boxes of each of the books, 
and returns a list of cropped images. Setting ```visualise=True```, the following two images give an example. 
```python
model, class_names = model_init(config, weights, coco_names)
cropped = crop_books(model, img, visualise=True) 
```
![book bounding boxes and cropped book](https://github.com/chadgoldsworthy/yolo_book_recommender/blob/main/readme_imgs/crop_books.png?raw=true)

These cropped images are then passed into the ```extract_books()``` function which uses pytesseract to extract the text text from the images. Setting ```visualise=True```, the following image gives an example. 

```python
ISBNs, metas, authors = extract_books(cropped, visualise=True)
```

![pytesseract predictions on cropped book](https://github.com/chadgoldsworthy/yolo_book_recommender/blob/main/readme_imgs/extract_books.png?raw=true)


Following this, the text is cleaned > converted to ISBN > back to author and meta data > searched via Google Books API > recommendation collection > and so on. Please refer to the notebook for the full implementation. 

Any questions can be directed to <a >chadgoldsworthy@gmail.com</a>
