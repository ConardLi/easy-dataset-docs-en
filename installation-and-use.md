---
icon: desktop-arrow-down
---

# Installation and Use

Currently, Easy Dataset supports three startup methods: client, NPM, and Docker. All methods **process data completely locally**, so you don't need to worry about data privacy issues.

### Client Startup (Suitable for Beginners)

To solve various local deployment environment issues, you can directly use the client to start, supporting the following platforms:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NmVkMTkyZjk3ZWU1MzA4ODc0YTI3ZDQyODhiOTNlYzVfTHd2c2hoYzNabTNJWlcwM1NzOWxncFk1SDlUMHV2NVNfVG9rZW46V01DbWI2NG54b2lVTEN4WHZGZmNMZUpUbnBjXzE3NDcxMzQ3MjA6MTc0NzEzODMyMF9WNA" alt=""><figcaption></figcaption></figure>

You can directly go to [https://github.com/ConardLi/easy-dataset/releases](https://github.com/ConardLi/easy-dataset/releases) to download the installation package suitable for your system:

<figure><img src=".gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

***

### NPM Startup (Suitable for Developers)

This project is built on Next, so as long as you have a Node environment locally, you can start directly through NPM. This is suitable for developers who need to debug the project:

1. Clone the repository:

```bash
   git clone https://github.com/ConardLi/easy-dataset.git
   cd easy-dataset
```

2. Install dependencies:

```bash
   npm install
```

3. Start the server:

```bash
   npm run build
   npm run start
```

{% hint style="warning" %}
Note: When using NPM startup, when the system releases a new version, you need to re-execute `git pull` to fetch the latest code, and then re-execute the three steps of `npm install`, `npm run build`, and `npm run start`.
{% endhint %}

***

### Docker Startup (Suitable for Private Deployment)

If you want to build the image yourself for deployment in cloud services or intranet environments, you can use the `Dockerfile` in the project root directory:

1. Clone the repository:

```bash
   git clone https://github.com/ConardLi/easy-dataset.git
   cd easy-dataset
```

2. Build the Docker image:

```bash
   docker build -t easy-dataset .
```

3. Run the container:

```bash
   docker run -d -p 1717:1717 -v {YOUR_LOCAL_DB_PATH}:/app/local-db --name easy-dataset easy-dataset
```

> **Note:** Please replace `{YOUR_LOCAL_DB_PATH}` with the actual path where you want to store the local database.
