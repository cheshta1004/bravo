# bravo
const express = require('express');
const _= require("lodash");
const { exec } = require('child_process');
const app = express();
const port = 3000;

app.get(`/api/blog-stats' , (req, res) => {
  const Command = `curl --request GET \
    --url https://intent-kit-16.hasura.app/api/rest/blogs \
    --header 'x-hasura-admin-secret: 32qR4KmXOIpsGPQKMqEJHGJS27G5s7HdSKO3gdtQd2kv5e852SiYwWNfxkZOBuQ6'`;

  exec(Command, (error, out) => {
    if (error) {
      Console.error(error);
      return res.status(500).json({ error: 'Error  at server side' });
    }

    const Data = JSON.parse(out);
const totalBlogs = _.get(Data, 'posts.length', 0);

// Find the blog with the longest title
const blogWithLongestTitle = _.maxBy(Data.posts, 'title.length');

const blogsWithTitle = _.filter(Data.posts, post => _.includes(post.title.toLowerCase(), 'privacy'));

const uniqueBlogTitles = _.uniq(_.map(blogData.posts, 'title'));
 
    res.json(responseData);
  });
});



app.get('/api/blog-search', (req, res) => {
  const { query } = req.query; // Get the query parameter from the URL

  if (!query) {
    return res.status(400).json({ error: `Query ${query} is unsupported` });
  }

  const filteredBlogs = Data.posts.filter(post =>
    post.title.toLowerCase().includes(query.toLowerCase())
  );

  res.json(filteredBlogs);
});

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
