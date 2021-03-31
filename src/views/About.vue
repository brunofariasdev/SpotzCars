<template>
  <div class="about">
    <div class="info-about">
        <h3>About</h3>
      <div class="info-content">
        <div class="text">
          <h5>Title Lorem Ipsum</h5>
          <p> 
            Lorem ipsum dolor sit amet. Aut dolor accusantium non voluptas dolorem et ratione repellat et unde exercitationem 33 necessitatibus totam qui excepturi consequatur. <br>
            Ut autem temporibus et omnis sint ut exercitationem necessitatibus qui eius corrupti aut consequuntur rerum est quis deleniti. Et earum corrupti rem nisi odit ea nulla magni non officiis alias et vero porro. <br>
          </p>
          <p>
            Aut aspernatur eaque et delectus enim et quaerat quod est voluptatem iste quo iusto eius id nihil totam.<br>
            Est voluptas porro quo rerum optio qui commodi commodi et animi aspernatur ut ratione eveniet cum galisum consequatur.<br>
            Et repellat obcaecati cum quis enim sit neque provident aut placeat rerum.<br>
          </p>
        </div>
        <div class="text">
          <p>
            Sed itaque maxime est inventore galisum est autem quod.
            Vel tenetur dolorem sit magnam eveniet et excepturi quis ab quia temporibus quo harum natus est Quis omnis. 
            Est obcaecati nesciunt sed doloribus beatae aut omnis commodi. 
          </p>
          <p>
            Est voluptates facilis sed quos eligendi et atque quidem aut suscipit placeat aut galisum eum magnam minima quo inventore voluptas.<br>
            Cum dicta dolorem et impedit laboriosam sed placeat galisum in culpa recusandae At sapiente enim est odio quaerat et odio adipisci.<br>
            Vel laudantium quia et rerum omnis ut unde quam quo earum placeat quo impedit vero.<br>
            Id quasi voluptatum ad consequuntur velit ea repellendus maiores aut dolore dolores sit voluptatibus ipsum qui eius illum! <br>
          </p>
        </div>
      </div>
    </div>
    <div class="team">
      <h2>Our<span>Team</span></h2>
      <div class="container-team">
        <div class="profile">
          <img src="https://www.brasilvagasexecutivas.com.br/arquivos/capa_cursos/executivo.jpg" alt="">
          <h4>CEO</h4>
          <h3>George Brown </h3>
        </div>
        <div class="profile">
          <img src="https://demo.vehica.com/wp-content/uploads/2020/10/p2-1-336x284.jpg" alt="">
          <h4>Principal</h4>
          <h3>Jacob Austin </h3>
        </div>
        <div class="profile">
          <img src="https://demo.vehica.com/wp-content/uploads/2020/10/p6-1-336x284.jpg" alt="Marcela">
          <h4>Product manager</h4>
          <h3>Emily Rees</h3>
        </div>
      </div>
    </div>  
    <footer>
      <a href="#">Política de Privacidade</a>
      <div class="redes">
        <i class="fab fa-facebook"></i>
        <i class="fab fa-instagram-square"></i>
        <i class="fab fa-twitter"></i>
      </div>
    </footer>
  </div>
</template>
<style scoped>
.about{
  height: inherit;
  width: 100%;
  background-position: start;
  background-size: cover;
  background: url('https://demo.vehica.com/wp-content/uploads/2020/10/bg-1920-new.jpg');
}
.info-content{
  display: flex;
  flex-direction: row;
  padding: .5rem;
  height: 14rem;
  max-width: 60rem;
  background-color: var(--blue);
}
.text{
  padding: .1rem;
}
.text:last-child{
  margin-top: 1.3rem;
}
.text h5{
  color: var(--orange);
  font-size: 1.1rem;
}
.info-about{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 8rem;
}
.info-about h3{
  padding: .3rem;
  color: var(--blue);
  font-size:2rem;
}
.info-about p{
  text-align: start;
  color: var(--black);
  padding: .4rem;
  font-size: .8rem;
  font-weight: 600;
}
.team{
  background-color: var(--black-contrast);
  width: auto;
}
.team h2{
  padding-top: .4rem;
  font-size: 2rem;
  color: var(--orange);
}
.team span{
  color: var(--grey);
  padding-left: .3rem;
}
.container-team{
  display: flex;
  flex-direction: row;
  height: 19rem;
  flex-wrap: wrap;
  justify-content: center;
  background: var(--black-contrast);
}
.profile{
  height: 8rem;
  width: 10rem;
  margin: 2rem;
}
.profile img{
  height: 8rem;
  width: 8rem;
  border-radius: 50%;
  border: white 3px solid;
  margin: .4rem;
}
.profile h3{
  color: white;
  padding: .3rem;
}
footer{
  background-color: var(--blue);
  width: 100%;
  height: 10rem;
  flex-direction: column;
  display: flex;
  align-items: center;
  justify-content: center;
}
footer a{
  text-decoration: none;
  color: var(--black);
  font-size: 1rem;
  cursor: pointer;
}
.redes{
  height: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 1.3rem;
}
.redes i{
  color: var(--black);
  padding: .4rem;
  cursor: pointer;
  font-size: 2rem;
}

@media (max-width: 400px){
  .info-content{
    height: auto;
  }
}
@media (max-width: 900px){
  .info-content{
    height: auto;
  }
}
@media(max-width: 670px){
  .team{
    height: 30rem;
    padding: 1rem;
  }
}
@media(max-width: 480px){
  .team{
    height: 45rem;
  }
}
</style>

