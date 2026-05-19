# IMY 210 Assignment 3 Reflection

## GitHub Repository
https://github.com/Anti1810/imy210_a3

## Commands to Run the Project

### Backend (Strapi)
```bash
cd backend
docker build -t blog-backend .
docker run -p 1337:1337 --env-file .env blog-backend
```

### Frontend (Nuxt)
```bash
cd frontend
docker build -t blog-frontend .
docker run -p 3000:3000 blog-frontend
```

## Reflection

Strapi Works really well as a Headless CMS. I found it really easy to  get it set up and manage it.
It is really easy to make changes on the fly if something is not working for me, which I really appreciate.
Docker did not feel nearly as good to work with. I struggled alot to get it working properly.
It had a lot of classes which annoyed me alot. I had alot of Node version mismatches using it.
This assignment also reinforced how I feel about JAMSTACK. Its a great approach to development.
NUXT Also felt really good to use and work with.