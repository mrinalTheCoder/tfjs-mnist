# MNIST Digit using TensorFlow JS
I trained a model for MNIST digot recognition and saved the keras model as an .h5 file. Then converted that model into both TensorFlow JS Graph model and TensorFlow Layers model to demonstrate how easy it is to use tensorflow with javascript. I have used both the models to predict hand written digits and display the predictions on the web page.

### Converting models
I used the `tensorflowjs_converter` to convert the model from .h5 to the required formats. <br/>
To convert to TensorFlow JS Graph model: <br/><br/>
`tensorflowjs_converter  --output_format tfjs_graph_model --input_format keras mnist_model.h5 ./model_graph`<br/><br/>
To convert to TensorFlow JS Layers model: <br/><br/>
`tensorflowjs_converter  --output_format tfjs_layers_model --input_format keras mnist_model.h5 ./model_layers`<br/><br/>
The above commands created the model in the [model_graph](https://github.com/mrinalTheCoder/tfjs-mnist/tree/master/model_graph) and [model_layers](https://github.com/mrinalTheCoder/tfjs-mnist/tree/master/model_layers) directories respectively.

### Setting up environment
I ran the code in Chrome browser on my local machine. This required to launch a web server from my machine otherwise I ran into CORS issues. I started a python web server in the base directory where we checkout this code as: <br/><br/>
`python3 -m http.server`

### HTML file
The `<head>` loads tfjs and defines the charset, title, etc. I have added an image in the `<body>` that corresponds to the digit 7. In the `<script>`, the img is first converted to a Tensor. Then, 2 async tasks are defined, one for the graph model and the other for the layers model. They load the models, run the prediction, log the output to the console and return the output. Both were successfully able to predict the digit correctly.

### Loading the model
We use async programming in javascript, the model is loaded from the .json file using `tf.loadGraphModel` as follows:<br/<<br/>
`async () => {
    const model = await tf.loadGraphModel("model_graph/model.json");
}`

### Prediction
To make the prediction, invoke the `predict` method on the model loaded above as follows: <br/><br/>
`const predictions_graph = await model.predict(inp_data.toFloat());`<br/><br/>
`predictions_graph` will have the predictions for the JS Graph model, hence the name.

### Digit Recognition
The above prediction will give a tensor with the probablity of each digit as predicted by the model. So, we need to run `argMax` on the predictions to get the digit with the maximum probability as follows:<br/><br/>
`predictions_graph.argMax(1)`<br/><br/>
However, the above returns a Tensor. To return the digit:<br/><br/>
`return predictions_layers.argMax(1).dataSync()[0];`
