https://github.com/gcrodrigues/github-repositories-finder


api.js
```
import axios from "axios";

const api = axios.create({
  baseURL: "https://api.github.com/users",
});

export default api;
```
-----

index.js

```
import api from "./api";

export const fetchRepos = async (user) => {
  if (user === "") {
    return;
  }

  try {
    const { data } = await api.get(`/${user}/repos`);

    const response = data.map((data) => {
      const {
        name,
        description,
        html_url,
        stargazers_count,
        watchers_count,
        forks_count,
      } = data;

      const modifiedData = {
        name,
        description,
        url: html_url,
        star: stargazers_count,
        watch: watchers_count,
        forks: forks_count,
      };

      return modifiedData;
    });

    return response;
  } catch (error) {
    console.log(error);
  }
};

export const fetchUserInfo = async (user) => {
  const { data } = await api.get(`/${user}`);

  const {
    avatar_url,
    login,
    html_url,
    name,
    bio,
    public_repos,
    followers,
    following,
  } = data;

  const response = {
    avatar: avatar_url,
    login,
    url: html_url,
    name,
    bio,
    repos: public_repos,
    followers,
    following,
  };
  return response;
};
```
------
components/users/users.jsx
```
const User = () => {
  const { userInfoValue, loadingValue } = useContext(Context);
  const [userInfo, setUserInfo] = userInfoValue;
  const [loading, setLoading] = loadingValue;
  ```
-----
components/repository/repository.jsx
```
const Repository = ({ name, description, url, watch, star, forks }) => {
  const { sizeValue } = useContext(Context);
  const [size, setSize] = sizeValue;

  function handleNumberFormat(value) {
    const convertedNumber = value.toString();

    if (value >= 1000 && value < 10000) {
      return convertedNumber.split("", 2).join(".") + "k";
    } else if (value >= 10000) {
      return convertedNumber.split("", 2).join("") + "k";
    }
    return value;
  }
  ```
  
