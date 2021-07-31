https://github.com/melboudali/Github-User-Search

./src/app.js  (imports first all the components for the app.js)
  
```
const App = () => {
  const githubState = useContext(GithubContext);
  const { searchAllUsers } = githubState;

  useEffect(() => {
    searchAllUsers();
    // eslint-disable-next-line
  }, []);
```
-----
```
const Users = () => {
  const githubState = useContext(GithubContext);
  const { users, ResultCount, loading } = githubState;

  return (
    <Fragment>
      {ResultCount > 30 && <h6>{ResultCount} users found.</h6>}
      {loading ? (
        <Spinner />
      ) : (
        <Row>
          {users.map(user => (
            <UserComp key={user.id} user={user} />
          ))}
        </Row>
      )}
    </Fragment>
  );
};
export default Users;
```

```
const UserPage = props => {
  const githubState = useContext(GithubContext);
  const { match } = props;
  const {
    user: {
      name,
      avatar_url,
      followers,
      following,
      location,
      email,
      bio,
      company,
      blog,
      public_repos,
      public_gists,
      html_url,
      hireable
    },
    searchUser,
    loading,
    getRepos,
    joined,
    statusCode
  } = githubState;

  useEffect(() => {
    searchUser(match.params.login);
    getRepos(match.params.login);
    // eslint-disable-next-line
  }, []);
  ```
-----

```
const ReposPage = () => {
  const githubState = useContext(GithubContext);
  const { repos } = githubState;

  return (
    <Fragment>
      {repos.map(repo => (
        <ReposComp key={repo.id} repo={repo} />
      ))}
    </Fragment>
  );
};

export default ReposPage;
```

```
const ReposComp = props => {
  const {
    name,
    html_url,
    description,
    stargazers_count,
    watchers_count,
    forks_count,
    language,
    updated_at,
    license
  } = props.repo;

  const uDate = updated_at.split("-");
  ```
