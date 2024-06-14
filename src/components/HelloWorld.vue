<template>
  <div class="navbar">
    <!-- Icône du hamburger menu -->
    <div class="hamburger" @click="toggleMenu">
        <span></span>
        <span></span>
        <span></span>
    </div>

    <div class="navbar-title">Faire mon diagnostic RGPD&nbsp;&nbsp;Calculer mes économies</div>
    
    <img src="../assets/logo.png" alt="Logo" class="navbar-logo">
    <ul  class="menu">
      <li v-for="item in menuItems" :key="item.label"
          @mouseover="showSubMenu(item.label)"
          @mouseout="hideSubMenu">
        <a href="#" class="menu-link">{{ item.label }}</a>
        <span v-if="['Solution', 'Service', 'Entreprise', 'Ressources'].includes(item.label)" class="arrow down"></span>
        <div v-if="item.submenu && hoveredItem === item.label" class="submenu">
          <div v-for="column in item.submenu" :key="column.toString()" class="submenu-column">
            <a v-for="subItem in column" :key="subItem.title" href="#" class="submenu-item">
                <div class="submenu-title">{{ subItem.title }}</div>
                <p class="submenu-description">{{ subItem.description }}</p>
            </a>
          </div>
        </div>
      </li>
    </ul>
    <div class="right-section">
      <span>Contactez-nous 02 55 99 32 91</span>
      <span class="INN">in</span>
      <a href="URL_DE_CONNEXION">Se connecter</a>
    </div>
    <div class="buttons">
      <button class="btn1">Essai gratuit</button>
      <button class="btn2">Demander une démo</button>
    </div>
  </div>

  <!-- Menu pour les appareils mobiles -->
  <ul v-if="isMenuOpen" class="mobile-menu">
      <li v-for="item in menuItems" :key="item.label">
          <a href="#" @click="showSubMenu(item.label)">{{ item.label }}</a>
          <ul v-if="item.submenu && hoveredItem === item.label">
              <li v-for="column in item.submenu" :key="column.toString()">
                  <a v-for="subItem in column" :key="subItem.title" href="#">
                      {{ subItem.title }}
                  </a>
              </li>
          </ul>
      </li>
  </ul>
</template>



<script>
export default {
    data() {
        return {
            hoveredItem: null,
            menuItems: [
                {
                    label: 'Solution',
                    submenu: [
                        [
                            { title: 'Centre de formation', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',  },
                            { title: 'Campings', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',},
                            { title: 'Associations', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.', },
                            { title: 'Ressources humaines', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',  }
                        ],
                        [
                            { title: 'Experts comptables', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',  },
                            { title: 'E-commerce', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.', },
                            { title: 'Immobilier', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.', },
                            { title: 'Conseil', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',  }
                        ]
                        // Add more arrays here if necessary
                    ]
                },
                { label: 'Service' },
                { label: 'Entreprise' },
                { label: 'Ressources' },
                { label: 'Blog' }
                
            ],
            isMenuOpen: false 
        };
    },
    methods: {
        showSubMenu(label) {
            this.hoveredItem = label;
        },
        hideSubMenu(event) {
            // Check if the cursor is still inside the <li> element or the submenu
            if (!event.relatedTarget || 
                (event.relatedTarget && !event.currentTarget.contains(event.relatedTarget))) {
                this.hoveredItem = null;
            }
        },
        toggleMenu() {  // Ajoutez cette méthode ici
            this.isMenuOpen = !this.isMenuOpen;
        }
    }
}
</script>



<style scoped>



.arrow {
      border: solid #00ea99;
    border-width: 0 2px 2px 0;
    display: inline-block;
    padding: 2px;
}

.down {
        transform: rotate(45deg);
    -webkit-transform: rotate(45deg);
    margin-left: 5px;
    vertical-align: middle;
    position: absolute;
    right: 5px;
    top: 44%;
   
}




.mobile-menu li ul {
    list-style-type: none;
    padding-left: 20px;
}


@media only screen and (min-width: 580px)and (max-width: 1920px){
    .mobile-menu{
        display: none  !important;
    }
}

.mobile-menu {
    list-style-type: none;
    padding: 0;
    display: flex;
    
   
flex-direction: column;
}

.mobile-menu li {
    padding: 10px;
    border-bottom: 1px solid #eee;
}


.hamburger {
    display: none; /* Initially hide it. Will show on mobile */
    flex-direction: column;
    cursor: pointer;
    
   
gap: 5px;
}

.hamburger span {
    background-color: #000;
    height: 3px;
    width: 25px;
}

@media (max-width: 576px) {
    .hamburger {

       margin-left: -110%; 
        
       
display: flex;
    }

    .navbar {
        display: none; /* Hide navbar on mobile */
    }

.right-section{
    display: none !important;
}

.navbar-title{
    display: none !important;
}

.btn1{
    display: none !important;
}

.menu{
    display: none !important;
}




.navbar-logo{
    display: none !important;
}

.btn2{
    display: none !important;
}


    /* Mixin */
/* reset */
* {
  padding: 0;
  margin: 0;
}

.navbar {
  
  height: 50px;
  margin-top: 1% !important;
  padding: 0 16px;
  display: flex;
  align-items: center;
  background-color: #ffffff00 !important;
}

.m-menu__checkbox {
  display: none;
}

.m-menu__toggle {
  cursor: pointer;
  flex: none;
}

.m-menu {
  position: absolute;
  top: 0;
  left: 0;
  max-width: 450px;
  width: calc(100vw - 30px);
  height: 100%;
  transform: translate3d(-450px, 0, 0);
  transition: transform 0.35s;
  z-index: 1;
  overflow: hidden;
  background-color: #fff;
}

.m-menu__overlay {
  background-color: rgba(103, 103, 103, 0.5);
  position: absolute;
  top: 0;
  width: 100%;
  bottom: 0;
  z-index: 1;
  display: none;
}

.m-menu__header {
  padding: 0 16px;
  height: 50px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #e8e8e8;
}

.m-menu__header span {
  font-size: 1.2rem;
  font-weight: bold;
  text-align: center;
  width: 100%;
}

.mobile-menu {
  height: 100%;
  overflow-y: auto;
  
}



.mobile-menu li a,
.mobile-menu li label {
  display: block;
  text-align: left;
  padding: 0 15px;
  line-height: 47px;
  text-decoration: none;
  color: #ffffff;
  cursor: pointer;
  font-size: 1rem;
  border-bottom: 1px solid #e8e8e8;
  position: relative;
}

.mobile-menu li label.a-label__chevron::after {
  content: "";
  position: absolute;
  display: inline-block;
  height: 10px;
  width: 10px;
  border-color: #333;
  border-style: solid;
  border-width: 1px 1px 0 0;
  transform: rotate(45deg);
  top: 50%;
  margin-top: -5px;
  right: 16px;
}

.wrapper {
  width: 480px;
  height: 667px;
  margin: 0 auto;
  overflow: hidden;
  background-color: #fff;
  position: relative;
}

body {
  background-color: #f1f1f1;
  padding: 0;
  margin: 0;
  font-family: sans-serif;
}




}

.submenu-item .submenu-title {
        font-family: 'Montserrat', sans-serif;
    color: #302E44;
    text-align: left;
    font-size: 15px;
    line-height: 1.5;
    margin: 0;

    
font-family: Montserrat;
font-size: 14px;
font-style: normal;
font-weight: 800;
line-height: 18px; /* 128.571% */
}

/* Tablet */
@media (max-width: 992px) { /* Adjust the breakpoint as per your design */
    .submenu-item .submenu-title {
        font-size: 15px;
    }
}

/* Mobile */
@media (max-width: 576px) { /* Adjust the breakpoint as per your design */
    .submenu-item .submenu-title {
        font-size: 14px;
    }
}

.submenu-item {
    display: block;
    padding: 5px 10px;
    text-decoration: none;
    color: #333;
    transition: background-color 0.3s;

    
}

.submenu-item:hover {
    background-color: #eee;
}

.submenu-description {
    text-align: left;
    margin: 0; 
    font-size: 13px;
    color: rgba(47, 46, 65, 0.80);
font-family: Montserrat;
position: relative;
top: 6px;
font-size: 10px;
font-style: normal;
font-weight: 400;
line-height: 15px; /* 150% */
}



.submenu-description {
    font-family: 'Montserrat', sans-serif;
    font-weight: 400; /* Regular */
    line-height: 1.5; /* 150% */
}

/* Desktop */
.submenu-description {
    font-size: 13px;
}

/* Tablet */
@media (max-width: 992px) { /* Adjust the breakpoint as per your design */
    .submenu-description {
        font-size: 14px;
    }
}

/* Mobile */
@media (max-width: 576px) { /* Adjust the breakpoint as per your design */
    .submenu-description {
        font-size: 12px;
    }
}



.chevron-down::before {
        content: '';
    border-style: solid;
    border-width: 2px 2px 0 0;
    display: inline-block;
    vertical-align: middle;
    position: relative;
    color: #00EA99;
    left: 4px;
    top: -2px;
    width: 7px;
    height: 7px;
    transform: rotate(135deg);
}

.submenu-column {
    padding: 10px;
    margin-left: 2%;
    margin-top: 3%;
    flex: 1;
}

.submenu-column:last-child {
  border-right: none;
}

.submenu-column a:hover {
  background-color: #eee;
}

.submenu-column a {
  display: block;
  padding: 5px 10px;
  text-decoration: none;
  color: #333;
  transition: background-color 0.3s;
}


.menu li.has-arrow::after {
  content: " \2193"; 
  margin-left: 5px; 
  display: inline-block;
  transform: scale(0.7);
}

.menu-link {
     display: flex;
    color: #302E44;
    font-family: Montserrat;
    font-size: 14px;
    font-style: normal;
    font-weight: 500;
    line-height: normal;
    
}





.right-section {
    align-self: flex-end;
    display: flex;
    position: relative;
    top: -3px;
    left: -5.1%;
    font-size: 13px;
    align-items: center;
    gap: 9px;
    color: #302E44;
    font-family: Montserrat;
    font-size: 11px;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
}

.right-section span, 
.right-section a {
    font-family: 'Montserrat', sans-serif;
    color: #000;
    margin-right: 20px;
}

.INN{
 font-weight: 700;
    font-size: 20px;
}

.right-section a {
  text-decoration: none;
  transition: color 0.3s;
}

.right-section a:hover {
  color: #2980b9;  /* Changer la couleur au survol */
}


  .navbar{
    display: flex;
    flex-direction: column;
    margin-top: -11%;
    margin-left: 6.1%;
    width: 86%;
    padding: 20px;
    background-color: white;
    border-radius: 28px;
    justify-content: space-between;
    
    }

.buttons {
    align-self: flex-end;
    display: flex;
    gap: 20px;
    left: -6%;
    top: -6px;
    position: relative;
    margin-top: 17px;
}

.btn1 {
        padding: 10px 22px;
    background-color: #ffffff;
    color: #302E44;
    cursor: pointer;
    border: 2px solid #302E44;
    border-radius: 8px;
    font-family: 'Montserrat', sans-serif;
    font-weight: 700;
    font-size: 16px;
    line-height: 1.5;
}

.btn2 {
        padding: 10px 22px;
    background-color: #23E59F;
    color: #302E44;
    cursor: pointer;
    border: none;
    border-radius: 8px;
    font-family: 'Montserrat', sans-serif;
    font-weight: 700;
    font-size: 20px;
    line-height: 1.5;
}

.btn:hover {
  background-color: #2980b9;
}

.navbar-logo {
    display: block;
    margin: 0 auto;
    position: relative;
    left: -1%;
    top: 157px;
    margin-top: -2%;
    width: 192px;
    height: 84px;
    flex-shrink: 0;

    
}



.menu {
    display: flex;
    list-style-type: none;
    padding: 0;
    position: relative;
    left: -21px;
    width: 701px;
    flex-wrap: inherit;
    transform: translateY(111px) translateX(128px);
}




.menu li {
  position: relative;
  margin-right: 7px;
}

.menu li a {
      display: block;
    padding: 11px 20px;
    
    color: #000000;
    text-decoration: none;
    transition: background-color 0.3s;
}

.menu li a:hover,
.menu li a:focus {
  background-color: rgb(255, 255, 255)000;
}

.submenu {
    display: block;
    width: 775%;
    height: 1010%;
    position: absolute;
    top: 100%;
    left: -20%;
    background-color: #ffffff;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
    
}


.submenu li {
  display: inline-block; /* Affichage horizontal */
  margin-right: 10px;
}

.navbar-title {
    font-size: 14px;
    line-height: 1.5;
    position: relative;
    top: 157px;
    color: #302E44;
    font-family: Montserrat;
    font-size: 11px;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
    left: 6.6%;
    color: rgb(0, 0, 0);
    margin-right: auto;
    padding: 10px 20px;
}

/* Pour les tablettes */
@media (max-width: 768px) {
   .navbar-title {
       font-size: 14px;      /* Taille de police pour tablette */
   }
}

/* Pour les mobiles */
@media (max-width: 576px) {
   .navbar-title {
       font-size: 12px;      /* Taille de police pour mobile */
   }
}

.submenu li a {
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.submenu li a:hover {
  background-color: #ddd;
}

.menu li:hover .submenu {
  display: flex;
}
</style>



