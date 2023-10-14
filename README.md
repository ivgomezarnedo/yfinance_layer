# AWS Lambda Python Layer with [`yfinance`](https://github.com/ranaroussi/yfinance)

This repository contains an AWS Lambda Layer that has the [`yfinance`](https://github.com/ranaroussi/yfinance) package, optimized for AWS Lambda use. It allows AWS Lambda functions to utilize  [`yfinance`](https://github.com/ranaroussi/yfinance) without bundling it with the function deployment package.

## Table of Contents

- [Quick Start](#quick-start)
- [Available ARNs](#available-arns)
- [Using the Layer](#using-the-layer)
- [Layer Contents](#layer-contents)
- [Deployment](#deployment)


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


**See [Deployment](#deployment) section with the details on how to deploy it in another region**

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

Got it. Let's refine that section to specify the incompatibility issues with `urllib3` as it relates to `boto3`:


## Layer Contents

This AWS Lambda Layer is meticulously crafted for users looking to exploit the capabilities of the `yfinance` library within the AWS Lambda environment. Here's a detailed insight into the Layer's contents and their significance:

### 1. **YFinance**:
A robust Python module, `yfinance` facilitates fetching financial data with ease. It permits developers to effortlessly pull stock market and other financial datasets into their applications. This library is paramount for numerous finance-centric applications, especially those operating in serverless environments like AWS Lambda.

### 2. **pysqlite3**:
The Python environment in AWS Lambda bundles an older version of `sqlite3`. This poses a challenge as `yfinance` capitalizes on window functions, which are unsupported by this legacy version. To circumvent this and fully harness the capabilities of `yfinance`, we've incorporated `pysqlite3` into this Layer. This package provides an updated version of `sqlite3` that aligns seamlessly with the requirements of `yfinance`.

### 3. **Exclusion of urllib3**:
An observant user might note the absence of `urllib3`, a standard dependency for `yfinance`, in this Layer. The rationale behind this decision is twofold:

   - `yfinance`'s version of `urllib3` was clashing with the version that `boto3` (which comes bundled by default with Lambda's Python environment) uses. This incompatibility could lead to unforeseen issues during execution.
   
   - AWS Lambda's Python environment naturally includes its own variant of `urllib3`. By steering clear of incorporating an overlapping and potentially conflicting version, we've chosen to trust Lambda's inherent `urllib3`.

## Deployment

If the provided Layer ARN isn't available in your AWS region, or you want to have your own private deployment, you can deploy the Layer yourself. Here's a step-by-step guide:

### Creating a New Layer Using the Release:

1. **Clone the repo**.

2. **ZIP the `python` folder**.

3. **Log in to AWS Management Console**: Open the AWS Management Console and navigate to the AWS Lambda service.

4. **Create a New Layer**:
   - Upload the zip file to S3.
   - Copy the S3 path of the uploaded file.
   - Click on "Layers" in the left navigation panel.
   - Click on "Create layer".
   - Provide a name for the layer.
   - Type the previously copied S3 path.
   - Select the appropriate runtime (Python 3.10).
   - Add a description (optional) and click on "Create".

5. Once the Layer is created, AWS will provide an ARN for the Layer. Note this down as you'll need it to use the Layer in your Lambda functions and possibly to contribute back to this repository.

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
