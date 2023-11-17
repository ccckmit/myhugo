# 第一個 Hugo 網站

## 參考

* [Hugo: Quick start](https://gohugo.io/getting-started/quick-start/)


這篇文章有兩個錯誤

    錯誤 echo "theme = 'ananke'" >> hugo.toml 

    應該改為 echo theme = 'ananke' > hugo.toml

    也就是 hugo.toml 的內容應該是 theme = 'ananke'

第二個錯誤是，最後的 hugo 指令，不會將貼文建置到 public 資料夾下，必須加上 --buildDrafts 才會將貼文放入 public，所以應該用

    hugo --buildDrafts

* [Hugo: Host on GitHub Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

    Publish the site 這段

    其中的 .github/workflows/hugo.yaml 內容原本 run 這段是

        run: |
        hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"  

    應該要改為

        run: |
          hugo \
            --buildDrafts \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"

也就是加上 --buildDrafts 參數，否則的話會沒有任何貼文，因為沒有把草稿放上去！

這種使用 github action 的方式，我們不需要每次都在命令列去下 hugo --buildDrafts 指令

只要設定好 github action，之後每次 push 上去，github 就會自動幫我們建置，省時省力省 CPU！


