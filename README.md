# Optical Character Recognition model using Keras, TenserFlow, OpenCV
![Diagram](https://www.pyimagesearch.com/wp-content/uploads/2020/08/ocr_handwriting_reco_header.png)
## Intoduction 

   Optical character recognition or optical character reader (OCR) is the  conversion of images of typed, handwritten or printed text into machine-encoded text, whether from a scanned document, a photo of a document, a scene-photo (for example the text on signs and billboards in a landscape photo) or from subtitle text superimposed on an image. 


## Getting Started
1. Install all following requirements from requirements.txt:
   ```bash
   #With pip
   pip install -r requirements.txt
   ```
   After this command, keras-ocr, tenserflow, opencv(v4.2.0.34), flask will be installed in your environment 
    
2. Then clone our repository:  
   ```bash
   # Clone git repo
   git clone {} 
   ```
3. To run project, execute following commands in terminal:

   Step 1: Open the server with 
   ```
   python app.py
   ```
   The server is setup on port 5000.

   Step 2: Open the front end page.

   If you want to use python.
   ```
   // python3
   python -m http.server
   // python2
   python -m SimpleHTTPServer
   ```
   If you prefer Node.js
   ```
   npm install serve -g // install serve
   serve // this will open a mini web serve
   // or http-serve
   npm install http-server -g
   http-server
   ```
    
## Project descriptions
   Poject use **keras-ocr, tenserflow, opencv** for creating OCR model and **flask** for creating web-application.

### OCR 
   Keras is an open-source library that provides a Python interface for artificial neural networks. Keras acts as an interface for the TensorFlow library.
   OCR pipline consists of two parts **Detector and Recogniser** 
   ```
   ```
### Server part

Since flask is very simple and wroted by python, we build it with only a few lines of code.

This function receive base64 encoded image from front end page, converted it to PIL Image, then do the object detection step.

```
@app.route('/api/', methods=["POST"])
def main_interface():
    response = request.get_json()
    data_str = response['image']
    point = data_str.find(',')
    base64_str = data_str[point:]  # remove unused part like this: "data:image/jpeg;base64,"

    image = base64.b64decode(base64_str)       
    img = Image.open(io.BytesIO(image))

    if(img.mode!='RGB'):
        img = img.convert("RGB")
    
    # convert to numpy array.
    img_arr = np.array(img)

    # do object detection in inference function.
    results = inference(sess, detection_graph, img_arr, conf_thresh=0.5)
    print(results)

    return jsonify(results)
```

### Front end part
In front end page, with the help of  jQuery ajax, we can send the base64 image to backend, wait for the result, then draw the bounding box on the page.

Core code is:
```
// handle image files uploaded by user, send it to server, then draw the result.
function parseFiles(files) {
  const file = files[0];
  const imageType = /image.*/;
  if (file.type.match(imageType)) {
    warning.innerHTML = '';
    const reader = new FileReader();
    reader.readAsDataURL(file);
    reader.onloadend = () => {
      image.src = reader.result;
      // send the img to server
      communicate(reader.result);
    }
  } else {
    setup();
    warning.innerHTML = 'Please drop an image file.';
  }
}
```

## More examples  
  ![](https://imgur.com/tLlfk1I.png)
  
  ![](https://imgur.com/LN41ooq.png)
  
  ![](https://imgur.com/KbxPIvr.png)
 
## 
## Authors

* **Bolotov Heorgii** - *Initial work* - [BeefMILF](https://github.com/BeefMILF)
* **Moroz Denis** - *Initial work* - [HPMortys](https://github.com/HPMortys)

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/BeefMILF/OCR-KPI-PetProject/blob/master/LICENSE) file for details

## References




   
