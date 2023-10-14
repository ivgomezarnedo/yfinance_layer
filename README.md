# AWS Lambda Python Layer with `yfinance`

This repository contains an AWS Lambda Layer that has the [`yfinance`](https://github.com/ranaroussi/yfinance) package, optimized for AWS Lambda use. It allows AWS Lambda functions to utilize  [`yfinance`](https://github.com/ranaroussi/yfinance) without bundling it with the function deployment package.

## Table of Contents

- [Quick Start](#quick-start)
- [ARN Details](#available-arns)
- [Using the Layer](#using-the-layer)

## Quick Start

To use this layer in your AWS Lambda function:

1. Navigate to AWS Lambda in the AWS Management Console.
2. Create or select an existing function.
3. Under the `Layers` section, choose `Add a Layer`.
4. Select `Provide a layer version ARN` and input the ARN provided below.
5. Save and deploy your function.

## Available ARNs 

The ARN for the layer is:

| Region    | ARN |
|-----------| --- |
| us-west-2 | ```arn:aws:lambda:us-west-2:100957474272:layer:yfinance_layer:5``` |


**You can deploy it in another region**

## Using the Layer

Once you've added the layer to your Lambda function, you can import and use  [`yfinance`](https://github.com/ranaroussi/yfinance) just like you would in any Python script:

```python
ad.user_cache_dir = lambda *args: "/tmp" # Lambda
import yfinance as yf

def lambda_handler(event, context):
    ticker = yf.Ticker("AAPL")
    hist = ticker.history(period="5d")
    return hist.to_dict()
```

I understand. Let's adjust the instructions accordingly by referencing the ARN table in the `README.md` and guiding users to update it with new ARNs for other regions:

---

## Deployment

If the provided Layer ARN isn't available in your AWS region, or you want to have your own private deployment, you can deploy the Layer yourself. Here's a step-by-step guide:

### Creating a New Layer Using the Release:

1. **Download the Release**: Navigate to the "Releases" section of this repository. Download the latest release zip file, which contains the `yfinance` package optimized for Lambda.

2. **Log in to AWS Management Console**: Open the AWS Management Console and navigate to the AWS Lambda service.

3. **Create a New Layer**:
   - Click on "Layers" in the left navigation panel.
   - Click on "Create layer".
   - Provide a name for the layer.
   - Click on "Upload" and choose the downloaded release zip file.
   - Select the appropriate runtime, likely "Python 3.x".
   - Add a description (optional) and click on "Create".

4. Once the Layer is created, AWS will provide an ARN for the Layer. Note this down as you'll need it to use the Layer in your Lambda functions and possibly to contribute back to this repository.

### Contributing the ARN for a New Region:

If you deploy this Layer in a new region and wish to contribute the ARN to help others:

1. **Fork the Repository**: Click on the "Fork" button on the top-right corner of this repository page.

2. **Clone Your Forked Repository**:
   ```bash
   git clone [URL of your forked repository]
   ```

3. **Update the ARN Table in README.md**: Navigate to the `README.md` file in your cloned repository. Add the ARN for the new region to the existing table.


4. **Commit and Push Your Changes**:
   ```bash
   git add README.md
   git commit -m "Added ARN for [region-name]"
   git push origin main
   ```

5. **Send a Merge Request (MR)**: Go back to the main page of your forked repository on GitHub. Click on "New Pull Request". Ensure the base repository is set to the original repository (not your fork) and the base branch is `main`. Fill out the necessary details and submit the pull request.

Once your MR is reviewed and merged, the new ARN will be available in the main repository's README.md, benefitting all users looking for that specific region.
