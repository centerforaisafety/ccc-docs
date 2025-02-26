# Storage

## **How to use the global Hugging Face model cache**

The CAIS cluster provides a global Hugging Face model cache to facilitate efficient access to popular resources without affecting your file system quota. This cache is maintained by the CAIS cluster administrators and is regularly updated with frequently used models. Below is a guide on how to utilize this resource.

### **Accessing the Global Cache**
The global Hugging Face cache is located at `/data/huggingface/`. You can use the cache by either setting the `cache_dir` argument or by setting the `HF_HOME` environment variable. For example:

```sh
import torch
from transformers import AutoModelForCausalLM, AutoTokenizer

cache_dir = "/data/huggingface/"
model_name = "meta-llama/Meta-Llama-3-8B-Instruct"

print("Loading model...")
model = AutoModelForCausalLM.from_pretrained(model_name, device_map="auto", cache_dir=cache_dir)
tokenizer = AutoTokenizer.from_pretrained(model_name, cache_dir=cache_dir)
```

### **Requesting Models to be Added to the Cache**
If you require a model that is not already cached, you can request it by posting in the #shared-models Slack channel. Please include the full name, such as `meta-llama/Meta-Llama-3.1-8B`. Requests are typically processed within 24 hours, subject to approval.

!!! tip "You can view the list of models currently available in the global cache on our [Shared Models Tracker](https://docs.google.com/spreadsheets/d/1q8q1vWuEqaZixtX_XTy0HNIAv8b9zBim_zVRDCLcmfI/edit?gid=0#gid=0)."

### **Cache Maintenance and Updates**
The global cache is updated regularly, with popular models added automatically. Models that have not been used for over 60 days will be removed.

### **Troubleshooting**
Here are some common issues and how to resolve them:

| Issue/Message               | Advice                                                                                                           |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Model Not Found**         | Double-check the model name for typos. Refer to the Shared Models Tracker for the correct path.                  |
| **Missing Dependencies**    | Ensure all required Python packages are installed.                                                               |
| **Missing Token**           | Obtain and configure the required authentication token for models that need it. Refer to Hugging Face docs.      |
| **Need More Help?**         | Reach out via the **#shared-models-data** Slack channel for further assistance.                                  |

!!! tip "Using Custom Models"
    If you need to cache a custom model locally, feel free to make use of a local HF cache. However, be mindful of storage quotas and only use local caching when necessary.