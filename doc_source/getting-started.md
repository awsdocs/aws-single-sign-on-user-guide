# ขอให้<a name = "ต้อง"></a >
.. [รฺส']น . คอสตูม/กุล'SWITB
หัวข้อต่อไปนี้คือการรับชม
ศูนย์ข้อมูลการใช้งาน AMI
🔌..ออโต้..เอพีที่ตามมาไอรักไร้ทรัพย
...name: GitHub Actions Demo
run-name: ${{ github.actor }} is testing out GitHub Actions 🚀
บน: [กด]
งาน: ecosystem
  สาเหตุที่ขโมยมาจาก GitHub-: อำนาจของเจ้าของความเร็ว pangin a'i home run [ `]
    การทำงานบน: อู บุนตู ล่าสุด
    ขั้นตอน:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v3
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
**Topics**
+ [Prerequisites and considerations](get-started-prereqs-considerations.md)
+ [Step 1: Enable IAM Identity Center](get-started-enable-identity-center.md)
+ [Step 2: Create an administrative permission set](get-started-create-an-administrative-permission-set.md)
+ [Step 3: Choose your identity source and create an IAM Identity Center administrative user](get-started-choose-identity-source.md)
+ [Step 4: Set up AWS account access for additional users \(optional\)](set-up-single-sign-on-access-to-accounts.md)
+ [Step 5: Set up single sign\-on access to your applications \(optional\)](set-up-single-sign-on-access-to-applications.md)
