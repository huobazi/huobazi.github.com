
```bash
git clone git@github.com:huobazi/huobazi.github.com.git

git submodule add -f -b master git@github.com:huobazi/huobazi.github.com.git public

cd huobazi.github.com

git clone git@github.com:huobazi/purehugo.git

./deploy.sh
```