## Some work arounds

- To update outdated npm package run this command using bash
  ```
  npm outdated | awk 'NR>1 {print $1"@"$4}' | xargs npm install
