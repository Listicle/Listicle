<script context="module">
	import { setEnvironment } from '$houdini';
	import environment from '../environment';

	setEnvironment(environment);
</script>

<script>
	import Dashboard from '../components/Dashboard.svelte';
	import '../app.css';
  import { query, graphql } from '$houdini';
  
  const { data } = query(graphql`
    query getProjects {
      user(id:12) {
        id
        username
        projectsCount
        projects {
          id
          projectName
        }
      }
    }
  `)
	let projects = $data.user.projects;
</script>


<main class="flex flex-col items-center min-h-fit w-screen max-w-screen-xl font-sans text-sky-900 md:flex-row md:h-screen">
	<Dashboard {projects} />
	<slot />
</main>
