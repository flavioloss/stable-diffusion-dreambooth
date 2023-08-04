# Fine-tuning text to image model on custom dataset
This project showcase an implementation of the paper "DreamBooth: Fine Tuning Text-to-Image Diffusion Models for Subject-Driven Generation", using an image dataset of the character Walter White from Breaking Bad to finetune the Stable Diffusion model.

The main task for the fine-tuning is to provide an entity that could be a person or an object as training examples, and train the AI to generate images of that entity based on text prompts provided by the user. 

For requirments installation, run the first notebooks cells to clone the training python file from [Diffusers repository](https://github.com/huggingface/diffusers/tree/main). There are also some necessary libraries and specific versions that need installation, such as accelerate, transformers, bitsandbytes, gradio and huggingface_hub. The installation procedure can be executed by running the first notebook cells.

The next step is to define some variables. First, the model that was used ([stable-diffusion-v1-4](https://huggingface.co/CompVis/stable-diffusion-v1-4)) needs an authentication to a Hugging Face account, for license and model usability agreement. The model name is provided, alongside a data input directory. Two variables that compose the prompt are a token name, whitch is the name of the entity provided in the training examples, and the class name, whitch aggregates as a description for the token name. For the implemented example, the token name is Walter White (composed as w for the first name and the second name white) and the class name is man, since it's a feature associated to the entity. The next step is to upload files for the finetuning process, the paper sugest 6-8 images from different angles, entity face and face+body pictures. In this project, 9 images were uploaded.

Next the training begins, with a technique of image augmentation described in the paper and the actual model fine-tuning loop. The training cell uses accelarate to call the training py file, and some hyperparameters need to be defined. Several of these are kept as recommended in the paper, some are not. Training iterations for example, it's possible to use between 100 and 200 iterations per training image. Since there are 9 Walter White images, let’s use 1800 iterations. The model was fine-tuned in a free-tier Google Collab instance, so some parameters like using 8bit adam enabling  gradient checkpointing and setting gradient accumulation_steps to 1 were used to reduce GPU memory consumption.

The last part is the web application deployment of the fine-tuned model. Using the Gradio framework, it's possible to create an image generation web or notebook interface, where the user can input a custom prompt describing a situation or filter to apply to the entity used in the fine-tuning process. With Gradio, it's also possible to create a public server for anyone to access the model, but for basic usage reasons, the web server will run locally, as this is an evaluation project. 


### References
1. ["DreamBooth: Fine Tuning Text-to-Image Diffusion Models for Subject-Driven Generation"](https://paperswithcode.com/paper/dreambooth-fine-tuning-text-to-image)

2. [TryoLabs blog post](https://tryolabs.com/blog/2022/10/25/the-guide-to-fine-tuning-stable-diffusion-with-your-own-images)
