---
id: h5VPUrfE05MUVf6tiA4DC
title: Prompts for CLI
desc: ''
updated: 1627977269959
created: 1627977037534
---

- Used [prompts](https://www.npmjs.com/package/prompts) for adding prompts for cli 

```ts
const resp = await prompts({
          type: 'text',
          name: 'title',
          message: 'Do you want to overwrite: Yes/No',
          validate: title => ["yes", "no"].includes(title.toLowerCase())  ? true : `Enter either Yes or No` 
        });
console.log(resp.title)
```

