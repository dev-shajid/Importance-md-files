# Next Js

## useRouter - Link

```javascript
import { useRouter } from "next/router";
import Link from "next/link";

const router = useRouter();
const { id } = useRouter().query;
router.push("/");
```

## getServerSideProps

```javascript
export const getServerSideProps = async () => {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/posts?_limit=6`
  );
  const posts = await res.json();

  return {
    props: {
      posts,
    },
  };
};
```

## getStaticProps

```javascript
export const getStaticProps = async () => {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/posts?_limit=5`
  );
  const posts = await res.json();

  return {
    props: {
      posts,
    },
    revalidate: 10,
  };
};
```

## getStaticPaths

```javascript
export const getStaticPaths = async () => {
  const res = await fetch(
    "https://jsonplaceholder.typicode.com/posts?_limit=5"
  );
  const posts = await res.json();
  const ids = posts.map((post) => post.id);
  const paths = ids.map((id) => ({ params: { id: id.toString() } }));

  return { paths, fallback: false };
};
```
