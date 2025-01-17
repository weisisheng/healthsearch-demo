# 🔧 Healthsearch Demo - Backend 🔧

Welcome to the backend documentation for the Healthsearch Demo, designed to guide you through setting up, managing dependencies, and running this project.

## 📚 Documentation

The documentation will detail the steps needed to establish the backend component of the Healthsearch Demo, providing a comprehensive guide to the setup process and the operational aspects.

## 🗂️ Dataset

The `dataset_100_supplements.json` file contained in the `data` folder is intended to be imported into a Weaviate Cluster. This file serves as the primary data source for the demo, featuring product reviews, ratings, and health-related benefits of various supplements.

The backend expects the data to be in this format:

```
{
    "product_id": {
        "name": "Productname", # string
        "brand": "Productbrand", # string
        "rating": 4.5, # number
        "description": "Product description", # string
        "ingredients": "Product ingredients", # string
        "reviews": ["Example Review"], # list[string]
        "url": "URL to the product", # string
        "img": "URL to the product image", # string
        "summary": "Review summary", # string
        "effects": "Health effects", # string
    }
}
```
> For annotation functionality your own dataset in the frontend, encapsulate keywords like so: `<span className='annotation'> Keyword </span>`. This needs to be applied to the review field.

## 📦 Setup & Requirements

The following steps guide you through setting up the backend:

1. **Set up your Weaviate cluster:**
- **OPTION 1** Create a cluster in WCS (for more details, refer to the [Weaviate Cluster Setup Guide](https://weaviate.io/developers/wcs/guides/create-instance))
- **OPTION 2** Use Docker-Compose to setup a cluster locally [Weaviate Docker Guide](https://weaviate.io/developers/weaviate/installation/docker-compose)

2. **Set environment variables:**
- The following environment variables need to be set
- ```export WEAVIATE_SERVER_HEALTHSEARCH="http://your-weaviate-server:8080"```
- ```export WEAVIATE_KEY_HEALTHSEARCH="your-weaviate-database-key"```
- ```export OPENAI_API_KEY="your-openai-api-key"```
> You can use `.env` files (https://github.com/theskumar/python-dotenv) or set the variables to your system
> Note that if you're using the GPT-4 model (by default), ensure your OpenAI key has access.

3. **Create a new Python virtual environment:**
- Make sure you have python `>=3.8.0` installed
- ```python3 -m venv env```
- ```source env/bin/activate```

4. **Install dependencies:**
- The `requirements.txt` file lists the Python dependencies needed. Install these with the following command:
- ```pip install -r requirements.txt```

5. **Import dataset:**
- Use the provided script to import the dataset into Weaviate: `scripts/import_data_to_weaviate.py <FILENAME>`. If you wish to use your own dataset, ensure it matches the provided schema and adjust the API and Frontend accordingly.
> Note: The import script also deletes all classes if they already exist. This is handy for starting from scratch, but if you wish to append entries, a custom data ingestion script would be needed. More on this can be found [here](https://weaviate.io/developers/weaviate/manage-data/import).

6. **Start the FastAPI app:**
- ```uvicorn api:app --reload```

### 🐳 Using Docker

You can also use Docker to setup the backend. If you're not familiar with Docker you can read more about it here (https://docker-curriculum.com/)

Inside the backend folder, use these commands:

1. **Set environment variables:**
- The following environment variables need to be set
- ```export OPENAI_API_KEY="your-openai-api-key"```
> You can use `.env` files (https://github.com/theskumar/python-dotenv) or set the variables to your system
> Note that if you're using the GPT-4 model (by default), ensure your OpenAI key has access.
> Make sure that the Weaviate Key is empty and the Weaviate URL is set to `http://weaviate:8080`

2. **Run docker compose** 
-`docker-compose -f weaviate-docker-compose.yml up -d`

3. The database should now be exposed to the 8080 port. (OPTIONAL) Test the connection with 
-`curl -v http://localhost:8080/v1/.well-known/ready`

4. **Build the API docker image with**
-  `docker build -t healthsearch-backend .`

5. **Run the API docker with**
- `docker run -p 8000:8000 healthsearch-backend`

## 🔗 Code Maintanance

1. **Run Black for code formatting:**
-  `black api.py`
-  `black script/`

1. **Run mypy for type checking:**
-  `mypy api.py`
-  `mypy script/`

## 💖 Open Source Contribution

With these steps, you're ready to use and enhance the Health Search Demo backend. Happy coding!
Your contributions are always welcome! Feel free to contribute ideas, feedback, or create issues and bug reports if you find any! Please adhere to the code guidelines that include formatting, linting, and testing.



