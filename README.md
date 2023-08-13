const output = await replicate.run(
  "stability-ai/sdxl:2b017d9b67edd2ee1401238df49d75da53c523f36e363881e057f5dc3ed3c5b2",
  {
    input: {
      prompt: 'A rainbow colored tiger',
      negative_prompt: 'ugly, soft, blurry, out of focus, low quality, garish, distorted, disfigured',
      image: 'https://replicate.delivery/pbxt/JF3foGR90vm9BXSEXNaYkaeVKHYbJPinmpbMFvRtlDpH4MMk/out-0-1.png',
      prompt_strength: 0.8,
      width: 1024,
      height: 1024,
      num_inference_steps: 50,
      scheduler: 'DDIM',
      guidance_scale: 7.5,
      refine: 'base_image_refiner',
      refine_steps: '20'
    }
  }
);
import openai_secret_manager

assert "openai" in openai_secret_manager.get_services()
secrets = openai_secret_manager.get_secret("openai")

import openai
openai.api_key = secrets["api_key"]

prompt = "a black giraffe with a lion's head"
response = openai.Image.create(prompt=prompt, n=1)
image_url = response['data'][0]['url']
