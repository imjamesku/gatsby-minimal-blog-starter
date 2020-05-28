---
title: Implementing Active Class for Links in Next.js
date: 2020-05-27T23:13:10.104Z
description: Implementing Active Class for Links in Next.js
keywords: next.js active link style
path: /blog/nextjs-active-link
slug: nextjs-active-link
tags:
  - next.js
  - 前端
  - 網頁開發
---
Since next.js does not have built-in solutions for active link styling, I spent some time looking for a concise way so implement it. This is the best one I've found so far. The code is written in typescript, but you can delete the types if you don't want to bother with the types.

## How to Use it
Just replace `Link`s with `NavLink` and pass in `activeClassName` as a prop and style the link with whatever `activeClassName` is.

```tsx
import React from 'react'
import Link from 'next/link'
import { useRouter } from 'next/router'

type Props = {
    href: string;
    children: any;
    activeClassName: string;
}

const NavLink =  ({ href, children, activeClassName}: Props) => {
  const router = useRouter()
  let className = children.props.className || ''
  if (router.pathname === href) {
    className = `${className} ${activeClassName}`
  }

  return <Link href={href}>{React.cloneElement(children, { className })}</Link>
}

NavLink.defaultProps = {
    activeClassName: 'selected'
} as Partial<Props>

export default NavLink
```

Example:
```jsx
<Link to="/" activeClassName="activeLink">Hello</Link>
```