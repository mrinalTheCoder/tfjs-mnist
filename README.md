# Convert a pre-trained model to tfjs layers model and tfjs graph model and perform predictions

### Converting models
I used the `tensorflowjs_converter` to convert the model from .h5 to the required formats. The excat command are:
`sudo tensorflowjs_converter  --output_format tfjs_graph_model --input_format keras mnist_model.h5 ./model_graph` for graph model and `sudo tensorflowjs_converter  --output_format tfjs_layers_model --input_format keras mnist_model.h5 ./model_layers` for layers model. The above commands created the model in the [model_graph](https://github.com/mrinalTheCoder/tfjs-mnist/tree/master/model_graph) and [model_layers](https://github.com/mrinalTheCoder/tfjs-mnist/tree/master/model_layers) directories respectively.

### Setting up environment
I ran the code in Chrome, and so I had to use a server to run. I initialised a server using the `python3 -m http.server` command.

### HTML file
The head loads tfjs and defines the charset, title, etc. I have added an image in the body (the digit 7). In the script, the img is first converted to a Tensor. Then, 2 async tasks are defined, one for the graph model and the other for the layers model. They load the models, run the prediction and log the output to the console. Both were successfully able to predict the digit correctly.
