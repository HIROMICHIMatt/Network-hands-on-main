## Before the hands-on lab  

Duration: 15 minutes

### Task 1: Create a Virtual Network (hub) with Subnets  
1.  Azure portalにアクセスし、 **+ Create a resource**をクリック。 **Search the Marketplace** から **Virtual Network** を選択し、 **Create**をクリック。

2.  **Basics** タブ上で以下の情報を入力。

    -  Subscription: **Choose your subscription**.

    -  Resource group: **Create new**をクリックし、 **SpokeVNetRG2**と入力。

    - Name: **SpokeVNet2**

    -  Region: **Japan East**

3.  以下のスクリーンショットのようになっていることを確認し、 **Next: IP Addresses**をクリック。

   ![](images/2021-10-09-11-21-41.png)

4. **IP Addresses**タブで以下の情報を入力。

    -  IPv4 address space: **10.8.0.0/20**

    -  **+ Add subnet**をクリックし、右に現れる**Add subnet**ブレードに以下の情報を入力後、**Add**をクリック。

       -  Subnet name: **AppSubnet**

       -  Subnet address range: **10.8.0.0/25**

5. 完了したら **Review + Create** に進み、**Create**をクリック。 

6.  SpokeVNetRG2 リソースグループに行き、**SpokeVNet2**ブレード下にある**Subnets** をクリック。(**Settings** セクションの下)

    ![](images/2021-10-09-11-30-27.png)

7.  **Subnets** ブレードにて、**+Subnet**をクリック。

    ![](images/2021-10-09-11-32-15.png)

8.  **Add subnet** ブレードにて、以下の情報を入力。

    -  Name: **DataSubnet**

    -  Address range: **10.8.1.0/25**

    -  Network security group: **None**

    -  Route table: **None**

9.  以下のように入力したら、 **Save** をクリック。

    ![](images/2021-10-09-11-34-05.png)

10. 設定が完了すると、以下のように見える。

     ![](images/2021-10-09-11-35-41.png) 

### Task 2: Use the Azure portal for a template deployment


1.  Labfileにある、**CloudShop.json**を自分のパソコンにダウンロードする。

2.  Azure portalにログイン状態であることを確認する( <http://portal.azure.com>)

3.  **+ Create a resource**をクリックし、**template deployment (deploy using custom templates)**を選択。

    ![](images/2021-10-09-11-42-27.png)

4.  **Template deployment (deploy using custom templates)** ブレードにて、**Create**をクリック。

5.  カスタムデプロイ ブレードにて、**Build your own template in the editor**をクリック。

    ![](images/2021-10-09-11-43-34.png)

6.  **Load file**をクリックし、 **CloudShop.json** を選択して **Save**をクリック。

    ![](images/2021-10-09-11-46-36.png)

7.  以下のパラメータにはこのテンプレートを過去に使った際の情報が入っているのでアップデートする。

    - Existing Virtual Network Name: **SpokeVNet2**
  
    - Existing Virtual Network Resource Group: **SpokeVNetRG2**
  
    - Web Subnet: **AppSubnet**
  
    - Data Subnet: **DataSubnet**

    ![](images/2021-10-09-11-49-21.png)

8.  また、空欄となっているリソースグループにも**SpokeVNetRG2**を選択。**Review + create** をクリックし、**Create**をクリック。このデプロイには30-40分かかります。

    -  Resource Group: Select **SpokeVNetRG2** you created earlier.

    -  Location: **Japan East** (The same location you used to provision resources earlier in this lab.)

    ![](images/2021-10-09-11-51-27.png)

### Task 3: Validate the CloudShop application is up after the deployment

1.  Azure portalから**SpokeVNetRG2** リソースグループを開き、デプロイを確認する。

2.  **WGWEB1** 仮想マシンをクリック。

3.  **WGWEB1** ブレードにて、 **Connect**をクリックした後、**RDP**を選択。 **Download RDP file** をし、Remote Desktopセッションを確立する。

    ![](images/2021-10-09-11-58-12.png)


4.  以下の情報を使ってログイン。

    -  User: **demouser**

    -  Password: **demo@pass123**

6.  以下の画面が出たら **Yes** を選択。

    ![](images/2021-10-09-12-00-43.png)

7.  以下が出たら**No**を選択。

    ![](images/2021-10-09-12-01-26.png)

8.  Server Managerがデフォルトで開くので、**Local Server**をクリック。

    ![](images/2021-10-09-12-02-22.png)

9.  **IE Enhanced Security Configuration** がオンになっていたら**Off**にする。

    ![](images/2021-10-09-12-03-47.png)

10. OffにするときはAdministratorsに対して**Off** にし、**OK**をクリック。

    ![](images/2021-10-09-12-04-26.png)

11. CloudShop application への接続を試すために、Internet Explorerを開き以下の2つにアクセスする。

    ```http
    http://wgweb1
    ```

    ```http
    http://wgweb2
    ```

You should follow all steps provided *before* performing the Hands-on lab.
