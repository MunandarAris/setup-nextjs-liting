######## Penejlasan Tentang Tools yang Akan Digunakan ########

1. Eslint adalah sebuah tools yang di gunakan untuk mengecek code javascript kita apakah ada kesalahan atau tidak

2. Prettier adalah sebuah tools yang digunakan untuk membuat aturan kepada codingan kita agar lebih rapih dan
   seragam

3.Husky adalah sebuah tools yang digunakan untuk menjalankan linting ( mengecek code kita apakah sudah sesuai
dengan aturan yang kita tentukan atau belum ) dan ini berjalan sebelum benar - benar melakukan sebuah perintah
git ( commit )

4. Lint Staged adalah sebuah tools yang akan membantu proses linting ( mengecek code kita apakah sudah sesuai
   dengan aturan yang kita tentukan atau belum ) dan hanya akan di terapkan kepada file yang ada perubahan saja
   sehingga ini akan mempercepat proses commit kita

######## Proses Config ########

1. install prettier dan eslint-config-prettier ( npm i --save-dev prettier eslint-config-prettier )

2. buat file config prettier dengan nama .prettierrc.json dan disini kita akan menambahkan beberapa aturan yang
   ingin kita terapkan di project kita. refernsi disini ( https://prettier.io/docs/en/options.html )
   contoh aturan yang akan kita terapkan => {
   "endOfLine": "lf",
   "printWidth": 80,
   "trailingComma": "es5",
   "semi": false,
   "jsxSingleQuote": true,
   "singleQuote": true,
   "useTabs": true,
   "tabWidth": 2,
   "arrowParens": "always"
   }

3. kemudian masuk ke file eslintrc.json dan tambahkan code berikut ini
   {
   "extends": ["eslint:recommended", "next", "prettier"]
   }

4. untuk setting up prettier dan linter sudah siap, code kita akan otomatis di perbaiki jika kita melakukan save
   jika kita sudah melakukan config di Format On Save jika menggunakan VS CODE atau code kita akan di perbaiki
   ketika kita menjalankan sebuah peritah, untuk itu masuk ke package.json kemudian di bagian scripts tambahkan
   code sebagai berikut "format": "prettier --write ."

5. selanjutnya kita akan menginstall husky dan lint-staged, ini bertujuan agar code kita di cek lagi ketika user
   melakukan commit, dimana ini sangat bermanfaat jika kita bekerja bersama tim dan ternyata tim kita tidak
   mengaktifkan Format On Save dan juga tidak menjalankan scripts "format": "prettier --write ."

6. untuk menginstall husky dan lint-staged gunakan perintah berikut ( npm i --save-dev husky lint-staged )

7. setelah itu silahkan masuk ke dalam file package.json lagi dan tambahkan code "prepare": "husky install" di
   scripts

8. kemudian jalankan perintahnya dengan npm run prepare, ini akan otomatis menginstall git hooks

9. masih di package.json di atas scripts tambahkan code berikut => "lint-staged": {
   "_.js": [
   "eslint --fix"
   ],
   "_.{html,js}": [
   "prettier --write"
   ]
   }

10. masih di package.json lagi tambahkan code "precommit": "lint-staged" di scripts

11. selanjutnya di terminal anda jalankan perintah berikut npx husky add .husky/pre-commit "npm run precommit"

12. dan akhirnya kita telah selesai melakukan configurasi untuk linting di aplikasi next js kita

13. kita tinggal menjalankan git commit -m "your message" dan linting kita akan otomatis berlajan
