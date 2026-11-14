import tkinter as tk
from tkinter import ttk, messagebox
from abc import ABC, abstractmethod
import logging

# ==========================================================
# ESTUDIANTE 1: ESTRUCTURA GENERAL, EXCEPCIONES Y CLIENTES
# ==========================================================

logging.basicConfig(
    filename="logs.txt",
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s",
    encoding="utf-8"
)

# Excepciones personalizadas
class ErrorSistema(Exception):
    pass

class DatoInvalidoError(ErrorSistema):
    pass

class ServicioNoDisponibleError(ErrorSistema):
    pass

class ReservaError(ErrorSistema):
    pass


# Clase abstracta general
class Entidad(ABC):
    @abstractmethod
    def mostrar_informacion(self):
        pass


# Clase Cliente con datos encapsulados
class Cliente(Entidad):
    def __init__(self, identificacion, nombre, correo):
       if not identificacion.strip() or not nombre.strip():
            raise DatoInvalidoError(
                "El documento y el nombre son obligatorios."
            )
        if not identificacion.isdigit():
            raise DatoInvalidoError(
                "El documento debe contener solo numeros."
            )

  self.__identificacion = identificacion
  self.__nombre = nombre
  self.__correo = ""

  self.correo = correo

  @property
  def identificacion(self):
    return self.__identificacion

  @property
  def nombre(self):
    return self.__nombre

  @property
  def correo(self):
    return self.__correo

  @correo.setter
  def correo(self, valor):
    if "@" not in valor or "." not in valor:
     raise DatoInvalidoError("El correo no es valido.")

  self.__correo = valor

  def mostrar_informacion(self):
     return (
        f"{self.identificacion} - "
        f"{self.nombre} - {self.correo}"
        )
            f"{self.nombre} - {self.correo}"
        )
