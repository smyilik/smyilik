[![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=smyilik&layout=compact)](https://github.com/smyilik/github-readme-stats)

https://user-images.githubusercontent.com/85386771/145724224-19691ed4-b712-498c-a182-c1049d723eb5.mp4

- name: Profile Readme Stats
  uses: teoxoy/profile-readme-stats@v1.2

on:
  schedule:
    - cron: '0 */12 * * *' # every 12 hours
  push:
    branches:
      - master
      - main
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
      with:
        fetch-depth: 0
    - name: Generate README.md
      uses: teoxoy/profile-readme-stats@v1
      with:
        token: ${{ secrets.USER_TOKEN }}
    - name: Update README.md
      run: |
        if [[ "$(git status --porcelain)" != "" ]]; then
        git config user.name github-actions[bot]
        git config user.email 41898282+github-actions[bot]@users.noreply.github.com
        git add .
        git commit -m "Update README"
        git push
        fi
