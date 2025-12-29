#### Introduction
Hi,I am ouse,Welcome to this repository.This is a demo that publish blazor-wasm to 
github pages.
#### Toturials
Thank for [jsakamoto‘s package](https://github.com/jsakamoto/PublishSPAforGitHubPages.Build)  
It has solved a lot of problems in publishing blazor-wasm to github pages.  
If you want to know this package's effect,please go this repository for more info!!!(Highly recommended!)
1. dotnet add package  PublishSPAforGitHubPages.Build
1. add this property to 	csproj
```xml
 <GHPages>true</GHPages>
```
3.  After confirming that the local test is successful, add a GitHub action.  
Replace your repository name in jobs-Publish
``` yaml
name: 部署到 GitHub Pages

on:
  push:
    branches: [ main ] # 只有当 main 分支有代码提交时才触发

jobs:
  deploy-to-github-pages:
    runs-on: ubuntu-latest
    steps:
      # 1. 检出代码
      - name: Checkout
        uses: actions/checkout@v4

      # 2. 安装 .NET SDK (根据你的项目版本修改，如 8.0)
      - name: Setup .NET
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '8.0.x'

      # 3. 发布项目 
      - name: Publish 
        run: dotnet publish  /PublishBlazorWASMToGithubPageDemo -c Release -o release

      # 4. 部署到 GitHub Pages 分支
      - name: Deploy
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          folder: release/wwwroot # 这是发布后的静态文件所在目录
          branch: gh-pages        # 部署到的目标分支
```
4. Open github-pages in your repository interface.
5. Visit your github pags and type  f12 for checking errors.

#### End
Thanks for your reading,if you have any problems,just let me know.