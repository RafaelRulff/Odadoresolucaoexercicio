# Odadoresolucaoexercicio

#include <stdio.h>

#include <stdarg.h>

#include <math.h>

#define GL_GLEXT_PROTOTYPES

#ifdef __APPLE__

#include <GLUT/glut.h>

#else

#include <GL/glut.h>

#endif

// ----------------------------------------------------------
// Funções Protótipos
// ----------------------------------------------------------

void display();

void specialKeys();

// ----------------------------------------------------------
// Variáveis Globais
// ----------------------------------------------------------

double rotate_y=0; 

double rotate_x=0;

// ----------------------------------------------------------
// display() Chamar função
// ----------------------------------------------------------

void display(){

  //  Clear screen and Z-buffer
  
  glClear(GL_COLOR_BUFFER_BIT|GL_DEPTH_BUFFER_BIT);

  // Reset transformations
  
  glLoadIdentity();
  
  // glTranslatef( 0.1, 0.0, 0.0 );      // Not included
  
  // glRotatef( 180, 0.0, 1.0, 0.0 );    // Not included

  // Rotate when user changes rotate_x and rotate_y
  
  glRotatef( rotate_x, 1.0, 0.0, 0.0 );
  
  glRotatef( rotate_y, 0.0, 1.0, 0.0 );
  
  // glScalef( 2.0, 2.0, 0.0 );          // Not included

  //Multi-colored side - FRONT
  
  glBegin(GL_POLYGON);
 
  glColor3f( 1.0, 0.0, 0.0 );     glVertex3f(  0.5, -0.5, -0.5 );      // P1 is red
  
  glColor3f( 0.0, 1.0, 0.0 );     glVertex3f(  0.5,  0.5, -0.5 );      // P2 is green
  
  glColor3f( 0.0, 0.0, 1.0 );     glVertex3f( -0.5,  0.5, -0.5 );      // P3 is blue
  
  glColor3f( 1.0, 0.0, 1.0 );     glVertex3f( -0.5, -0.5, -0.5 );      // P4 is purple
 
  glEnd();

  // White side - BACK
  
  glBegin(GL_POLYGON);
  
  glColor3f(   1.0,  1.0, 1.0 );
  
  glVertex3f(  0.5, -0.5, 0.5 );
  
  glVertex3f(  0.5,  0.5, 0.5 );
  
  glVertex3f( -0.5,  0.5, 0.5 );
  
  glVertex3f( -0.5, -0.5, 0.5 );
  
  glEnd();
 
  // Purple side - RIGHT
  
  glBegin(GL_POLYGON);
  
  glColor3f(  1.0,  0.0,  1.0 );
  
  glVertex3f( 0.5, -0.5, -0.5 );
  
  glVertex3f( 0.5,  0.5, -0.5 );
  
  glVertex3f( 0.5,  0.5,  0.5 );
  
  glVertex3f( 0.5, -0.5,  0.5 );
  
  glEnd();
 
  // Green side - LEFT
  
  glBegin(GL_POLYGON);
  
  glColor3f(   0.0,  1.0,  0.0 );
  
  glVertex3f( -0.5, -0.5,  0.5 );
  
  glVertex3f( -0.5,  0.5,  0.5 );
  
  glVertex3f( -0.5,  0.5, -0.5 );
  
  glVertex3f( -0.5, -0.5, -0.5 );
  
  glEnd();
 
  // Blue side - TOP
  
  glBegin(GL_POLYGON);
  
  glColor3f(   0.0,  0.0,  1.0 );
  
  glVertex3f(  0.5,  0.5,  0.5 );
  
  glVertex3f(  0.5,  0.5, -0.5 );
  
  glVertex3f( -0.5,  0.5, -0.5 );
  
  glVertex3f( -0.5,  0.5,  0.5 );
  
  glEnd();
 
  // Red side - BOTTOM
  
  glBegin(GL_POLYGON);
  
  glColor3f(   1.0,  0.0,  0.0 );
  
  glVertex3f(  0.5, -0.5, -0.5 );
  
  glVertex3f(  0.5, -0.5,  0.5 );
  
  glVertex3f( -0.5, -0.5,  0.5 );
  
  glVertex3f( -0.5, -0.5, -0.5 );
  
  glEnd();
 
  glFlush();
  
  glutSwapBuffers();
 
}

// ----------------------------------------------------------
// specialKeys() Chamar Função
// ----------------------------------------------------------

void specialKeys( int key, int x, int y ) {
 
  //  Right arrow - increase rotation by 5 degree
  
  if (key == GLUT_KEY_RIGHT)
  
    rotate_y += 5;
 
  //  Left arrow - decrease rotation by 5 degree
  
  else if (key == GLUT_KEY_LEFT)
  
    rotate_y -= 5;
 
  else if (key == GLUT_KEY_UP)
  
    rotate_x += 5;
 
  else if (key == GLUT_KEY_DOWN)
  
    rotate_x -= 5;
 
  //  Request display update
  
  glutPostRedisplay();
 
}


// main() function

int main(int argc, char* argv[]){
 
  
  glutInit(&argc,argv);
 
  
  glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH);
 
  
  glutCreateWindow("Awesome Cube");

  //  Enable Z-buffer depth test
  
  glEnable(GL_DEPTH_TEST);

  // Chamar Funções
  
  glutDisplayFunc(display);
  
  glutSpecialFunc(specialKeys);

  //  Pass control to GLUT for events
  
  glutMainLoop();
 
  //  Return to OS
  
  return 0;
 
}
