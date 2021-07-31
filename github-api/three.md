https://github.com/gauravgulati15/Search-Github-Users

```
const UserInfo = () => {
  const { githubUser } = React.useContext(GithubContext);
  const { public_repos, followers, following, public_gists } = githubUser;

  const items = [
    {
      id: 1,
      icon: <GoRepo className="icon" />,
      label: "repos",
      value: public_repos,
      color: "pink",
    },
    {
      id: 2,
      icon: <FiUsers className="icon" />,
      label: "followers",
      value: followers,
      color: "green",
    },
    {
      id: 3,
      icon: <FiUserPlus className="icon" />,
      label: "following",
      value: following,
      color: "purple",
    },
    {
      id: 4,
      icon: <GoGist className="icon" />,
      label: "gists",
      value: public_gists,
      color: "yellow",
    },
  ];
  
  return (
    <section className="section">
      <Wrapper className="section-center">
        {items.map((item) => (
          <Item key={item.id} {...item} />
        ))}
      </Wrapper>
    </section>
  );
};

const Item = ({ icon, label, value, color }) => {
  return (
    <article className="item">
      <span className={color}>{icon}</span>
      <div>
        <h3>{value}</h3>
        <p>{label}</p>
      </div>
    </article>
  );
};
```
-----

```
const Repos = () => {
  const { repos } = React.useContext(GithubContext);

  const languages = repos.reduce((total, item) => {
    const { language, stargazers_count } = item;

    if (!language) return total;
    if (!total[language])
      total[language] = { label: language, value: 1, stars: stargazers_count };
    else {
      total[language].value += 1;
      total[language].stars += stargazers_count;
    }

    return total;
  }, {});

  //most used language
  const mostUsed = Object.values(languages)
    .sort((a, b) => {
      return b.value - a.value;
    })
    .slice(0, 5);

  //most star per language
  const mostStar = Object.values(languages)
    .sort((a, b) => {
      return b.stars - a.stars;
    })
    .slice(0, 5)
    .map((item) => {
      return { ...item, value: item.stars };
    });
    
      // stars, forks
  let { stars, forks } = repos.reduce(
    (total, item) => {
      const { stargazers_count, forks, name } = item;
      total.stars[stargazers_count] = { label: name, value: stargazers_count };
      total.forks[forks] = { label: name, value: forks };
      return total;
    },
    {
      stars: {},
      forks: {},
    }
  );

  stars = Object.values(stars).slice(-5).reverse();
  forks = Object.values(forks).slice(-5).reverse();
```
