# Solar Shop ERP

Solar plates / inverter / battery dukaan ke liye poora software: stock, godown, Maal aaya (receipt), dispatch/invoice (GST + discount), employees aur salary.

## Chalane ka tareeka

Zaroorat: **Node.js 22 ya naya** (https://nodejs.org). Koi `npm install` nahi chahiye.

```
cd solar-erp
node server.js
```

Browser me kholein: `http://localhost:3000`

- Pehla login: **admin / admin123** (turant Settings me password badal lein)
- Port badalna ho: `PORT=8080 node server.js`

## Database kahan save hota hai

Sara data server par `data/solar.db` (SQLite) me save hota hai. Server band/chalu karne par bhi data rehta hai.
Is `data` folder ko hi backup karna hai (ya app me Settings -> Backup Download).

## Internet par (server/VPS) lagana

1. Kisi VPS (Ubuntu) par Node 22 install karein, `solar-erp` folder copy karein.
2. `npm i -g pm2 && pm2 start server.js --name solar-erp && pm2 save && pm2 startup`
3. Nginx reverse proxy + HTTPS (Let's Encrypt) lagayein taaki dukaan aur ghar dono jagah se chal sake.
4. `data/` folder ka roz backup (cron se) lein.

Dusre computer se usi network me chalana ho to `http://<server-ka-IP>:3000` kholein.

## Kya-kya hai

| Module | Kaam |
|---|---|
| Dashboard | Kul Maal, stock value, aaj/mahine ki bikri, lena-dena baki, kam stock alert |
| Products | Panel/inverter/battery etc., HSN, GST %, kharid-bikri rate, min stock |
| Stock & Godown | Godown-wise stock, opening stock, transfer, stock history |
| Maal Aaya (Receipt) | Supplier ka bill entry -> stock apne aap badhta hai |
| Dispatch / Invoice | Customer ko Maal bhejna -> stock ghatta hai, GST + discount ke saath invoice, print |
| Party | Customers / Suppliers, GSTIN, baki hisaab, payment entry |
| Employees | Staff ka record |
| Salary | Mahine ki salary, bonus, kata, advance, salary slip |
| Settings | Dukaan ka naam/GSTIN/bank/terms, password, backup |

## GST ke baare me

- Customer ka State dukaan ke State se alag ho to **IGST**, same ho to **CGST+SGST** lagta hai.
- Product ka GST % har product me alag set hota hai. Sahi rate aur HSN code apne CA se confirm kar lein.
- Discount poore bill par lagta hai (rupaye ya %) aur GST discount ke baad ke amount par judta hai.
- Invoice me total round-off hota hai aur amount shabdon me bhi chhapta hai.

## Invoice print

Bill ke saath **Print** dabayein -> naya page khulega (upar solar surya/panel wali banner, neeche saari details). "Print / PDF Save" se printer ya PDF dono ho sakte hain.

## Aage badhane ke liye (ideas)

Panel serial numbers, quotation, customer ledger statement, GSTR-1 export, WhatsApp par invoice bhejna, alag-alag users (staff/admin).
