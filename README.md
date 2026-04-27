# ABV Club Website

ABV Club 官方活動頁面，透過 GitHub Pages 發布。

## 網站網址

- Custom domain: <https://abvclub.com.tw>
- GitHub Pages fallback: <https://tellustek.github.io/abv-club-website/>

## 檔案結構

- `ABV_membership_official_launch_mobile_v2_links_precise.html`: 主要頁面來源檔。
- `.github/workflows/deploy-github-pages.yml`: GitHub Pages 自動部署流程。

## 部署方式

`main` branch 不直接放置 `index.html`。

當 `main` branch 有新的 push 時，GitHub Actions 會：

1. 建立 `public/` 目錄。
2. 將 `ABV_membership_official_launch_mobile_v2_links_precise.html` 複製為 `public/index.html`。
3. 產生 `public/CNAME`，內容為 `abvclub.com.tw`。
4. 將 `public/` 發布到 `gh-pages` branch。

GitHub Pages source 設定為：

```text
Branch: gh-pages
Path: /
```

## DNS 設定

`abvclub.com.tw` 需要指向 GitHub Pages：

```text
A      @     185.199.108.153
A      @     185.199.109.153
A      @     185.199.110.153
A      @     185.199.111.153
CNAME  www   tellustek.github.io
```

移除其他指向非 GitHub Pages 服務的 `@` A records，避免 custom domain 顯示 404 或被導到其他主機。

## 更新頁面

修改 `ABV_membership_official_launch_mobile_v2_links_precise.html` 後，提交並推送到 `main`：

```bash
git add ABV_membership_official_launch_mobile_v2_links_precise.html
git commit -m "fix: update club landing page"
git push
```

推送後 GitHub Actions 會自動更新 `gh-pages` branch。
