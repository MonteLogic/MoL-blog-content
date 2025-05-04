---
title: "Work Notes: Import CSV file into Prisma with Next.js 13+"
date: "2023-08-15"
---

This is the code I have so far but I don't feel like making a client component:

```
'use client'

import React, { useState } from 'react';
import csvParser from 'csv-parser';
import prisma from 'lib/prismadb';

const CSVImporter: React.FC = () => {
    const [importing, setImporting] = useState(false);

    const handleFileChange = async (event: React.ChangeEvent<HTMLInputElement>) => {
        const file = event.target.files?.[0];

        if (!file) return;

        setImporting(true);

        const reader = new FileReader();

        reader.onload = async (event) => {
            const csvData = event.target?.result as string;
            const transactions: any[] = [];

            csvParser()
                .on('data', (data) => {
                    transactions.push(data);
                })
                .on('end', async () => {
                    console.log('CSV file parsed:', transactions);

                    for (const transaction of transactions) {
                        await prisma.transactions.create({
                            data: {
                                date: new Date(transaction.Date),
                                num: transaction.Num,
                                payee: transaction.Payee,
                                memo: transaction.Memo,
                                category: transaction.Category,
                                amount: parseFloat(transaction.Amount),
                                balance: parseFloat(transaction.Balance),
                            },
                        });
                    }

                    console.log('Transactions imported successfully');
                    setImporting(false);
                    onImportSuccess();
                })
                .write(csvData);
        };

        reader.readAsText(file);
    };

    return (
        <div>
            <input
                type="file"
                accept=".csv"
                onChange={handleFileChange}
                disabled={importing}
            />
            <button onClick={() => { }} disabled={importing}>
                {importing ? 'Importing...' : 'Import Transactions'}
            </button>
        </div>
    );
};

export default CSVImporter;
```

My goal is to use an await and turn this into a server component so I can skip the API generation.

The Problem:

Okay, so I would like to look into a CSV file, get the information from it, get the information out of it and then send it into a database planning scale database. And I do all this with the app router.  
~

I am still trying to .... import transactions but then I found out about Plain banking so now I don't really need to. So I would only really do that import logic as like a learning thing. Also I want to add the Planetscale ORM.

My request object looks like this and it is a 200 but it responds with something went wrong and the values aren't updated.

```
[{"Date":"1/2/2023","Num":null,"Payee":"Fuelman Fuel Rebate","Memo":"POS PURCHASE FUELMAN FUEL REBATE FUELMAN FUEL REBATE N","Category":"Other Inc","Amount":0.2,"C":"c","Balance":0.2},{"Date":"1/3/2023","Num":null,"Payee":"Deposit","Memo":"Deposit # 1","Category":"Other Inc","Amount":5000,"C":"c","Balance":5000.2},{"Date":"1/3/2023","Num":null,"Payee":"Deposit M24-2424 W Iles Springfield-2424 W Isles Avenu","Memo":"DEPOSIT M24-2424 W ILES SPRINGFIELD-2424 W ISLES AVENU","Category":"Other Inc","Amount":1020,"C":"c","Balance":6020.2},{"Date":"1/3/2023","Num":null,"Payee":"Deposit","Memo":"Deposit # 1","Category":"Other Inc","Amount":1000,"C":"c","Balance":7020.2},{"Date":"1/3/2023","Num":null,"Payee":"Deposit","Memo":"Deposit SSA TREAS 310 XXSOC SEC","Category":"Taxes (Business)","Amount":526.7,"C":"c","Balance":7546.9}]
```

I need to figure out how to upload all of that.

But I think I'm going to put that on hibernate and then focus on **Plaid API** and importing transactions that way rather than this custom method I am trying with importing .csv.

I was unable to get this .csv thing working so now going to focus on the Plaid API.

View progress, [here](https://montelogic.com/?p=4348).

....

What I learned,

I learned that importing with a .csv requires making a call to the network which can be complicated and hard to replicate. If I were to add an abillity to export transactions, I would attach and ID column to the transactions so I know they aren't getting duplicated.
